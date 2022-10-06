---
title: Configurar os plug-ins do Editor de Rich Text
description: Saiba como configurar os plug-ins do Editor de Rich Text do Adobe Experience Manager para ativar funcionalidades individuais.
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
source-git-commit: 11cda989e6a28428f03a269c407a7672e6eab747
workflow-type: tm+mt
source-wordcount: '4406'
ht-degree: 5%

---


# Configurar os plug-ins do Editor de Rich Text {#configure-the-rich-text-editor-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade features . Você pode configurar a propriedade de recursos para ativar ou desativar, um ou mais recursos do RTE. Este artigo descreve como configurar especificamente os plug-ins do RTE.

Para obter detalhes sobre as outras configurações do RTE, consulte [Configurar o editor de rich text](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Ao trabalhar com o CRXDE Lite, é recomendável salvar as alterações regularmente usando [!UICONTROL Salvar tudo] opção.

## Ativar um plug-in e configurar a propriedade recursos {#activateplugin}

Para ativar um plug-in, siga estas etapas. Algumas etapas são necessárias apenas quando você configura um plug-in pela primeira vez, pois os nós correspondentes não existem.

Por padrão, `format`, `link`, `list`, `justify`e `control` plug-ins e todos os seus recursos são ativados no RTE.

>[!NOTE]
>
>Os respectivos `rtePlugins` nó é referido como `<rtePlugins-node>` para evitar a duplicação neste artigo.

1. Localize o componente de texto do seu projeto usando o CRXDE Lite.
1. Crie o nó pai de `<rtePlugins-node>` se não existir, antes de configurar qualquer plug-in do RTE:

   * Dependendo do seu componente, os nós principais são:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * um nó de configuração alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * São do tipo: **jcr:primaryType** `cq:Widget`
   * Ambos têm a seguinte propriedade:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valor** `./text`


1. Dependendo da interface para a qual você está configurando, crie um nó `<rtePlugins-node>`, se não existir:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Abaixo, crie um nó para cada plug-in que deseja ativar:

   * **Tipo** `nt:unstructured`
   * **Nome** a ID do plug-in do plug-in necessário

Depois de ativar um plug-in, siga estas diretrizes para configurar o `features` propriedade.

|  | Habilitar todos os recursos | Habilite alguns recursos específicos | Desativar todos os recursos |
|---|---|---|---|
| Nome | recursos | recursos | recursos |
| Tipo | Sequência de caracteres | String[] (multi-string; defina Tipo como String e clique em Multi in CRXDE Lite) | Sequência de caracteres |
| Valor | `*` (um asterisco) | definir para um ou mais valores de recurso | - |

## Entender o plug-in findreplace {#findreplace}

O `findreplace` O plug-in não precisa de configuração. Funciona imediatamente.

Ao usar a funcionalidade de substituição, a cadeia de caracteres de substituição a ser substituída deve ser inserida ao mesmo tempo que a cadeia de caracteres de localização. No entanto, você ainda pode clicar em localizar para procurar a cadeia de caracteres antes de substituí-la. Se a cadeia de caracteres de substituição for inserida após clicar em localizar, a pesquisa será redefinida para o início do texto.

A caixa de diálogo localizar e substituir se torna transparente quando a localização é clicada, e se torna opaca ao clicar em substituir. Isso permite que o autor revise o texto que será substituído. Se os usuários clicarem em substituir tudo, a caixa de diálogo será fechada e exibirá o número de substituições feitas.

## Configurar os modos de colagem {#paste-modes}

Ao usar o RTE, os autores podem colar o conteúdo em um dos três modos a seguir:

* **Modo de navegador**: Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode introduzir uma marcação indesejada.

* **Modo de texto sem formatação**: Cole o conteúdo da área de transferência como texto sem formatação. Remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir em [!DNL Experience Manager] componente.

* **Modo MS Word**: Cole o texto, incluindo tabelas, com formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou MS Excel, e manter apenas a formatação parcial.

### Configurar as opções de Colar disponíveis na barra de ferramentas do RTE  {#configure-paste-options-available-on-the-rte-toolbar}

É possível fornecer alguns, todos ou nenhum desses três ícones aos autores na barra de ferramentas do RTE:

* **[!UICONTROL Colar (Ctrl+V)]**: Pode ser pré-configurado para corresponder a um dos três modos Colar acima.

* **[!UICONTROL Colar como texto]**: Fornece a funcionalidade do modo de texto simples.

* **[!UICONTROL Colar do Word]**: Fornece a funcionalidade do modo MS Word.

Para configurar o RTE para exibir os ícones necessários, siga essas etapas.

1. Por exemplo, navegue até o seu componente `/apps/<myProject>/components/text`.
1. Navegar até o nó `rtePlugins/edit`. Consulte [ativar um plug-in](#activateplugin) se o nó não existir.
1. Crie o `features` na `edit` e adicione um ou mais recursos. Salve todas as alterações.

### Configure o comportamento do ícone e do atalho Colar (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Você pode pré-configurar o comportamento do **[!UICONTROL Colar (Ctrl+V)]** usando as etapas a seguir. Essa configuração também define o comportamento do atalho de teclado Ctrl+V que os Autores usam para colar o conteúdo.

A configuração permite os três tipos de casos de uso a seguir:

* Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode introduzir uma marcação indesejada. Configurado usando `browser` abaixo.

* Cole o conteúdo da área de transferência como texto sem formatação. Remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir AEM componente. Configurado usando `plaintext` abaixo.

* Cole o texto, incluindo tabelas, com formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou MS Excel, e manter apenas a formatação parcial. Configurado usando `wordhtml` abaixo.

1. No seu componente, navegue até `<rtePlugins-node>/edit` nó . Crie os nós se eles não existirem. Para obter mais informações, consulte [ativar um plug-in](#activateplugin).
1. No `edit` nó crie uma propriedade usando os seguintes detalhes:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Valor** Um dos modos de colagem necessários `browser`, `plaintext`ou `wordhtml`.

### Configurar os formatos permitidos ao colar o conteúdo {#pasteformats}

A palavra colar como Microsoft (`paste-wordhtml`) pode ser configurado mais detalhadamente para que você possa definir explicitamente quais estilos são permitidos ao colar em AEM de outro programa, como o Microsoft Word.

Por exemplo, se apenas formatos em negrito e listas forem permitidos ao colar em AEM, você poderá filtrar os outros formatos. Isso é chamado de filtragem de colagem configurável, que pode ser feita para ambos:

* [Texto](#paste-modes)
* [Links](#linkstyles)

Para links, também é possível definir os protocolos que são aceitos automaticamente.

Para configurar quais formatos são permitidos ao colar texto em AEM de outro programa:

1. No seu componente, navegue até o nó `<rtePlugins-node>/edit`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie um nó no `edit` nó para manter as regras de HTML paste:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Criar um nó em `htmlPasteRules`, para conter detalhes dos formatos básicos permitidos:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar os formatos individuais aceitos, crie uma ou mais das seguintes propriedades na `allowBasics` nó:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (para links e âncoras nomeadas)
   * **Nome** `image`

   Todas as propriedades são de **Tipo** `Boolean`, de acordo com as **Valor** você pode selecionar ou remover a marca de seleção para ativar ou desativar a funcionalidade.

   >[!NOTE]
   >
   >Se não estiver definido explicitamente, o valor padrão de true será usado e o formato será aceito.

1. Outros formatos também podem ser definidos usando uma variedade de outras propriedades ou nós, também aplicados à função `htmlPasteRules` nó . Salve todas as alterações.

Você pode usar as seguintes propriedades para `htmlPasteRules`.

| Propriedade | Tipo | Descrição |
|---|---|---|
| `allowBlockTags` | Sequência de caracteres | Define a lista de tags de bloco permitidas. Algumas tags de bloco possíveis incluem: <ul> <li>manchetes (h1, h2, h3)</li> <li>alínea p)</li> <li>listas (ol, ul)</li> <li>tabelas (tabela)</li> </ul> |
| `fallbackBlockTag` | Sequência de caracteres | Define a tag de bloco usada para qualquer bloco que tenha uma tag de bloco não incluída em `allowBlockTags`. `p` na maioria dos casos, é suficiente. |
| tabela | nt:unstructured | Define o comportamento ao colar tabelas. Esse nó deve ter a propriedade `allow` (digite Booleano) para definir se é permitido colar tabelas. Se permitir estiver definido como `false`, é necessário especificar a propriedade `ignoreMode` (digite String) para definir como o conteúdo da tabela colada é manipulado. Valores válidos para `ignoreMode` são: <ul> <li>`remove`: Remove o conteúdo da tabela.</li> <li>`paragraph`: Transforma células da tabela em parágrafos.</li> </ul> |
| list | nt:unstructured | Define o comportamento ao colar listas. Deve ter a propriedade `allow` (digite Boolean) para definir se a colagem de listas é permitida. If `allow` está definida como `false`, é necessário especificar a propriedade `ignoreMode` (digite String) para definir como lidar com qualquer conteúdo da lista colado. Valores válidos para `ignoreMode` são: <ul><li> `remove`: Remove o conteúdo da lista.</li> <li>`paragraph`: Transforma itens de lista em parágrafos.</li> </ul> |

Um exemplo de um `htmlPasteRules` A estrutura está abaixo.

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

## Configurar estilos de texto {#textstyles}

Os autores podem aplicar Estilos para alterar a aparência de uma parte do texto. Os estilos são baseados em classes CSS predefinidas na folha de estilos CSS. O conteúdo estilizado é delimitado em `span` tags que usam o `class` atributo para se referir à classe CSS. Por exemplo, `<span class=monospaced>Monospaced Text Here</span>`.

Quando o plug-in Estilos é ativado pela primeira vez, nenhum Estilo padrão está disponível. A lista pop-up está vazia. Para fornecer estilos aos autores, faça o seguinte:

* Habilite o seletor suspenso Estilo .
* Especifique a(s) localização(ões) da(s) folha(s) de estilos.
* Especifique os estilos individuais que podem ser selecionados na lista suspensa Estilo .

Para configurações posteriores, digamos para adicionar mais estilos, siga apenas as instruções para fazer referência a uma nova folha de estilos e especificar os estilos adicionais.

>[!NOTE]
>
>Você pode definir Estilos para [tabelas ou células de tabela](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Essas configurações exigem procedimentos separados.

### Ativar a lista suspensa Seletor de estilo {#styleselectorlist}

Isso é feito ativando o plug-in de estilos.

1. No seu componente, navegue até o nó `<rtePlugins-node>/styles`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `styles` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Salve todas as alterações.

>[!NOTE]
>
>Quando o plug-in Estilos estiver ativado, a lista suspensa Estilo será exibida na caixa de diálogo de edição. No entanto, a lista está vazia, pois nenhum Estilo está configurado.

### Especificar a localização da folha de estilos {#locationofstylesheet}

Em seguida, especifique a(s) localização(ões) da(s) folha(s) de estilos que deseja referenciar:

1. Navegue até o nó raiz do seu componente de texto, por exemplo `/apps/<myProject>/components/text`.
1. Adicionar a propriedade `externalStyleSheets` ao nó pai de `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (multi-string; click **Multi** no CRXDE)
   * **Valor(es)** O caminho e o nome de arquivo de cada folha de estilos que deseja incluir. Use caminhos do repositório.

   >[!NOTE]
   >
   >É possível adicionar referências a folhas de estilos adicionais a qualquer momento.

1. Salve todas as alterações.

>[!NOTE]
>
>Ao usar o RTE em uma caixa de diálogo (interface clássica), talvez você queira especificar folhas de estilos otimizadas para a edição de rich text. Devido a restrições técnicas, o contexto de CSS é perdido no editor, portanto, você pode querer emular esse contexto para melhorar a experiência de WYSIWYG.
>
>O Editor de Rich Text usa um elemento DOM de contêiner com uma ID de `CQrte` que podem ser usados para fornecer estilos diferentes para visualização e edição:
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### Especificar os Estilos disponíveis na lista pop-up {#stylesindropdown}

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/styles`, como criado em [Ativação do seletor suspenso de estilo](#styleselectorlist).
1. No nó `styles`, crie um novo nó (também chamado de `styles`) para manter a lista que está sendo disponibilizada:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crie um novo nó no `styles` nó para representar um estilo individual:

   * **Nome**, é possível especificar o nome, mas ele deve ser adequado para o estilo
   * **Tipo** `nt:unstructured`

1. Adicionar a propriedade `cssName` para este nó para fazer referência à classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valor** O nome da classe CSS (sem um &#39;.&#39; anterior; por exemplo, `cssClass` em vez de `.cssClass`)

1. Adicionar a propriedade `text` no mesmo nó; isso define o texto mostrado na caixa de seleção:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valor** Descrição do estilo; é exibida na caixa de seleção suspensa Estilo .

1. Salve as alterações.

   Repita as etapas acima para cada estilo necessário.

### Configurar o RTE para quebras de palavras ideais em japonês {#jpwordwrap}

Os autores que usam AEM para criar conteúdo em idioma japonês podem aplicar um estilo a caracteres para evitar quebras de linha, onde uma quebra não é necessária. Isso permite que os autores deixem as frases quebrarem na posição desejada. O estilo para essa funcionalidade é baseado na classe CSS predefinida na folha de estilos CSS.

>[!NOTE]
>
>Esse recurso requer pelo menos o AEM 6.5 Service Pack 1.

Para criar o estilo que os autores podem aplicar ao texto em japonês, siga estas etapas:

1. Crie um novo nó no nó estilos . Consulte [especificar um novo estilo](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Adicionar a propriedade `cssName` ao nó para fazer referência à classe CSS. Este nome de classe é um nome reservado para o recurso de quebra automática de texto em japonês.
   * Nome: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sem `.`)

1. Adicione o texto da propriedade ao mesmo nó. O valor é o nome do estilo que os autores veem ao selecionar o estilo.
   * Nome: `text`
*Tipo: 
`String`
   * Valor: `Japanese word-wrap`

1. Crie uma folha de estilos e especifique seu caminho. Consulte [especificar a localização da folha de estilos](#locationofstylesheet). Adicione o seguinte conteúdo à folha de estilos. Altere a cor do plano de fundo conforme desejado.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Folha de estilos para disponibilizar o recurso de quebra automática de texto em japonês para autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurar os formatos de parágrafo {#paraformats}

Qualquer texto criado no RTE é colocado em uma tag de bloco, sendo o padrão `<p>`. Ao ativar a `paraformat` , você especifica tags de bloco adicionais que podem ser atribuídas a parágrafos, usando uma lista suspensa de seleção. Os formatos de parágrafo determinam o tipo de parágrafo atribuindo a tag de bloco correta. O autor pode selecioná-los e atribuí-los usando o seletor de Formato. As tags de bloco de exemplo incluem, entre outras, o parágrafo padrão &lt;p> e rubricas &lt;h1>, &lt;h2>e assim por diante.

>[!CAUTION]
>
>Esse plug-in não é adequado para conteúdo com estrutura complexa, como listas ou tabelas.

>[!NOTE]
>
>Se uma tag de bloco, por exemplo, uma &lt;hr> não pode ser atribuído a um parágrafo, não é um caso de uso válido para um plug-in paraformat.

Quando o plug-in Formatos de parágrafo é ativado pela primeira vez, nenhum Formatos de parágrafo padrão é disponibilizado. A lista pop-up está vazia. Para fornecer aos autores Formatos de parágrafo, faça o seguinte:

* Habilite a lista suspensa Formatar seletor .
* Especifique as tags de bloco que podem ser selecionadas como formatos de parágrafo na lista suspensa.

Para configurações (re)posteriores, digamos para adicionar mais formatos, siga apenas a parte relevante das instruções.

### Ativar o seletor suspenso Formato {#formatselectorlist}

Primeiro habilite o plug-in paraformat:

1. No seu componente, navegue até o nó `<rtePlugins-node>/paraformat`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `paraformat` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
Se o plug-in não for configurado mais, os seguintes formatos padrão serão ativados:
* Parágrafo ( `<p>`)
* Cabeçalho 1 ( `<h1>`)
* Cabeçalho 2 ( `<h2>`)
* Cabeçalho 3 ( `<h3>`)
>


>[!CAUTION]
Ao configurar os formatos de parágrafo do RTE, não remova a tag de parágrafo &lt;p> como uma opção de formatação. Se a variável `<p>` for removida, o autor de conteúdo não poderá selecionar a variável **Formatos de parágrafo** mesmo se houver formatos adicionais configurados.

### Especificar os Formatos de Parágrafo disponíveis {#paraformatsindropdown}

Os formatos de parágrafo podem ser disponibilizados para seleção através de:

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/paraformat`, como criado em [Ativação do seletor suspenso de formato](#styleselectorlist).
1. Em `paraformat` criar um novo nó, para manter a lista de formatos:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crie um novo nó no `formats` , mantém os detalhes de um formato individual:

   * **Nome**, é possível especificar o nome, mas ele deve ser adequado para o formato (por exemplo, myparágrafo, myheader1).
   * **Tipo** `nt:unstructured`

1. Nesse nó, adicione a propriedade para definir a tag de bloco usada:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valor** A marca de bloco do formato; por exemplo: p, h1, h2, etc.

      Não é necessário inserir os colchetes delimitadores.

1. Para que o mesmo nó adicione outra propriedade, para que o texto descritivo apareça na lista suspensa:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valor** O texto descritivo desse formato; por exemplo, Parágrafo, Cabeçalho 1, Cabeçalho 2 e assim por diante. Este texto é exibido na lista de seleção Formato.

1. Salve as alterações.

   Repita as etapas para cada formato necessário.

>[!CAUTION]
Se você definir formatos personalizados, os formatos padrão (`<p>`, `<h1>`, `<h2>`e `<h3>`) são removidas. Recriar `<p>` como é o formato padrão.

## Configurar caracteres especiais {#spchar}

Em uma instalação padrão do AEM, quando a variável `misctools` está habilitado para caracteres especiais (`specialchars`) uma seleção por defeito é imediatamente disponibilizada para utilização; por exemplo, os símbolos de direitos autorais e de marcas registradas.

Você pode configurar o RTE para disponibilizar sua própria seleção de caracteres; definindo caracteres distintos ou uma sequência inteira.

>[!CAUTION]
Adicionar seus próprios caracteres especiais substitui a seleção padrão. Se necessário, (re)defina esses caracteres em sua própria seleção.

### Definir um caractere único {#definesinglechar}

1. No seu componente, navegue até o nó `<rtePlugins-node>/misctools`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `misctools` nó:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

          ou `String / *` se estiver aplicando todos os recursos para este plug-in)

1. Em `misctools` crie um nó para manter as configurações de caracteres especiais:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. Em `specialCharsConfig` crie outro nó para manter a lista de caracteres:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. Em `chars` adicione um novo nó para manter uma definição de caractere individual:

   * **Nome** é possível especificar o nome, mas ele deve refletir o caractere; por exemplo, metade.
   * **Tipo** `nt:unstructured`

1. Para esse nó, adicione a seguinte propriedade:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valor** Representação HTML do caráter requerido; por exemplo, `&189;` para a fração de metade.

1. Salve as alterações.

No CRXDE, depois que a propriedade é salva, o caractere representado é exibido. Veja abaixo o exemplo da metade. Repita as etapas acima para disponibilizar caracteres mais especiais para os autores.

![No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE](assets/chlimage_1-106.png "No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE")

### Definir um intervalo de caracteres {#definerangechar}

1. Use os passos 1 a 3 de [Definição de um caractere único](#definesinglechar).
1. Em `chars` adicione um novo nó para manter a definição do intervalo de caracteres:

   * **Nome** é possível especificar o nome, mas ele deve refletir o intervalo de caracteres; por exemplo, lápis.
   * **Tipo** `nt:unstructured`

1. Nesse nó (nomeado de acordo com o intervalo de caracteres especial), adicione as duas propriedades a seguir:

   * **Nome** `rangeStart`

      **Tipo** `Long`
      **Valor** o [Unicode](https://unicode.org/) representação (decimal) do primeiro caractere no intervalo

   * **Nome** `rangeEnd`

      **Tipo** `Long`
      **Valor** o [Unicode](https://unicode.org/) representação (decimal) do último caractere no intervalo

1. Salve as alterações.

   Por exemplo, definir um intervalo de 9998 - 10000 fornece os seguintes caracteres.

   ![No CRXDE, defina um intervalo de caracteres a serem disponibilizados no RTE](assets/chlimage_1-107.png)

   *Figura: No CRXDE, defina um intervalo de caracteres a serem disponibilizados no RTE*

   ![Caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up](assets/rtepencil.png "Caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up")

## Configurar estilos de tabela {#tablestyles}

Os estilos normalmente são aplicados no texto, mas um conjunto separado de Estilos também pode ser aplicado em uma tabela ou em algumas células da tabela. Esses Estilos estão disponíveis para os autores na caixa do seletor Estilo na caixa de diálogo Propriedades da célula ou Propriedades da tabela . Os estilos estão disponíveis ao editar uma tabela em um componente de Texto (ou derivado) e não no componente de Tabela padrão.

>[!NOTE]
Você pode definir estilos para tabelas e células somente para a interface clássica.

>[!NOTE]
Copiar e colar tabelas no componente RTE ou dele depende do navegador. Não é compatível imediatamente com todos os navegadores. Você pode obter resultados variados dependendo da estrutura da tabela e do navegador. Por exemplo, ao copiar e colar uma tabela em um componente RTE no Mozilla Firefox na interface clássica e na interface de toque, o layout da tabela não é preservado.

1. No componente, navegue até o nó `<rtePlugins-node>/table`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `table` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

   >[!NOTE]
   Se não quiser ativar todos os recursos da tabela, é possível criar a variável `features` propriedade como:
   * **Tipo** `String[]`
   * **Valor** s) Uma ou ambas, conforme exigido:
      * `table` para permitir a edição de propriedades de tabela; incluindo os estilos.
      * `cellprops` para permitir a edição de propriedades da célula, incluindo os estilos.


1. Defina o local das folhas de estilos CSS para referenciá-las. Consulte [Especificação do local da folha de estilos](#locationofstylesheet) já que isso é o mesmo que definir [estilos para texto](#textstyles). O local pode ser definido se você tiver definido outros estilos.
1. Em `table` criar os seguintes novos nós (conforme necessário):

   * Para definir estilos para a tabela inteira (disponível em **Propriedades da tabela**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Definição de estilos para células individuais (disponível em **Propriedades da célula**):

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Crie um novo nó (no `tableStyles` ou `cellStyles` (conforme apropriado) para representar um estilo individual:

   * **Nome** é possível especificar o nome, mas ele deve refletir o estilo.
   * **Tipo** `nt:unstructured`

1. Nesse nó, crie as propriedades:

   * Definição do estilo CSS a ser referenciado

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem uma `.`, por exemplo, `cssClass` em vez de `.cssClass`)
   * Definição de um texto descritivo a ser exibido no seletor suspenso

      * **Nome** `text`
      * **Tipo** `String`
      * **Valor** o texto a ser exibido na lista de seleção


1. Salve todas as alterações.

Repita as etapas acima para cada estilo necessário.

### Configurar cabeçalhos ocultos em tabelas para acessibilidade {#hiddenheader}

Às vezes, é possível criar tabelas de dados sem texto visual em um cabeçalho de coluna, supondo que a finalidade do cabeçalho seja implícita pelo relacionamento visual da coluna com outras colunas. Nesse caso, é necessário fornecer texto interno oculto na célula do cabeçalho para permitir que leitores de tela e outras tecnologias de assistência ajudem os leitores com várias necessidades a entender a finalidade da coluna.

Para aprimorar a acessibilidade em tais cenários, o RTE suporta células de cabeçalho ocultas. Além disso, ele fornece configurações relacionadas a cabeçalhos ocultos em tabelas. Essas configurações permitem aplicar estilos de CSS em cabeçalhos ocultos nos modos de edição e visualização. Para ajudar os autores a identificar cabeçalhos ocultos no modo de edição, inclua os seguintes parâmetros no código:

* `hiddenHeaderEditingCSS`: Especifica o nome da classe CSS aplicada na célula de cabeçalho oculta, quando o RTE é editado.
* `hiddenHeaderEditingStyle`: Especifica uma sequência de estilo que é aplicada na célula de cabeçalho oculta quando o RTE é editado.

Se você especificar o CSS e a sequência de estilo no código, a classe CSS terá prioridade sobre a sequência de estilo e poderá substituir qualquer alteração de configuração feita pela sequência de estilo.

Para ajudar os autores a aplicar o CSS em cabeçalhos ocultos no modo de visualização, é possível incluir os seguintes parâmetros no código:

* `hiddenHeaderClassName`: Especifica o nome da classe CSS aplicada na célula do cabeçalho oculta no modo de visualização.
* `hiddenHeaderStyle`: Especifica uma sequência de estilo que é aplicada na célula do cabeçalho oculto no modo de visualização.

Se você especificar o CSS e a sequência de estilo no código, a classe CSS terá prioridade sobre a sequência de estilo e poderá substituir qualquer alteração de configuração feita pela sequência de estilo.

## Adicionar dicionários para o verificador de ortografia {#adddict}

Quando o plug-in de verificação ortográfica é ativado, o RTE usa dicionários para cada idioma apropriado. Estes são então selecionados de acordo com o idioma do site, tirando a propriedade de idioma da subárvore ou extraindo o idioma do URL; por exemplo. o `/en/` a ramificação é verificada em inglês, a `/de/` ramificação como alemã.

>[!NOTE]
A mensagem `Spell checking failed` é visto se houver uma tentativa de verificação de um idioma que não esteja instalado. Os dicionários padrão estão localizados em `/libs/cq/spellchecker/dictionaries`, juntamente com os arquivos readme apropriados. Não modifique os arquivos.

Uma instalação de AEM padrão inclui os dicionários para inglês americano (`en_us`) e inglês britânico (`en_gb`). Para adicionar mais dicionários, siga estas etapas.

1. Navegar até a página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Siga um destes procedimentos para encontrar um dicionário de sua escolha de idioma:

   * Procure o dicionário de sua escolha de idioma. Na página do dicionário, localize o link para a página da Web da fonte original ou do autor. Localize os arquivos de dicionário da v2.x nessa página.
   * Procure por arquivos de dicionário v2.x em [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Baixe o arquivo com as definições de ortografia. Extraia o conteúdo do arquivo no seu sistema de arquivos.

   >[!CAUTION]
   Somente os dicionários na `MySpell` são compatíveis com o formato OpenOffice.org v2.0.1 ou anterior. Como os dicionários agora são arquivos de arquivamento, recomenda-se verificar o arquivo após o download.

1. Localize os arquivos .aff e .dic . Mantenha o nome do arquivo em minúsculas. Por exemplo, `de_de.aff` e `de_de.dic`.
1. Carregue os arquivos .aff e .dic no repositório em `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
O verificador ortográfico do RTE está disponível sob demanda. Ele não é executado automaticamente à medida que você começa a digitar o texto. Para executar o verificador ortográfico, clique em [!UICONTROL Verificador Ortográfico] na barra de ferramentas. O RTE verifica a ortografia das palavras e destaca as palavras com erro ortográfico.
Se você incorporar qualquer alteração sugerida pelo verificador ortográfico, o estado do texto será alterado e as palavras com erro ortográfico não serão mais destacadas. Para executar o verificador ortográfico, toque/clique no botão Verificador ortográfico novamente.

## Configure o tamanho do histórico para ações de desfazer e refazer {#undohistory}

O RTE permite que os autores desfaçam ou refaçam algumas últimas edições. Por padrão, 50 edições são armazenadas no histórico. Você pode configurar esse valor conforme necessário.

1. No componente, navegue até o nó `<rtePlugins-node>/undo`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `undo` nó criar a propriedade :

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valor** o número de etapas do comando desfazer que você deseja salvar no histórico. O padrão é 50. Use `0` para desabilitar completamente desfazer/refazer.

1. Salve as alterações.

## Configurar o tamanho da guia {#tabsize}

Quando o caractere de tabulação é pressionado dentro de qualquer texto, um número predefinido de espaços é inserido; por padrão, há três espaços sem quebra e um espaço.

Para definir o tamanho da guia:

1. No seu componente, navegue até o nó `<rtePlugins-node>/keys`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `keys` nó criar a propriedade :

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valor** o número de caracteres de espaço a serem usados para o tabulador

1. Salve as alterações.

## Definir margem de recuo {#indentmargin}

Quando o recuo estiver ativado (padrão), é possível definir o tamanho do recuo:

>[!NOTE]
O tamanho do travessão é aplicado somente aos parágrafos (blocos) do texto; não afeta o recuo das listas reais.

1. No componente, navegue até o nó `<rtePlugins-node>/lists`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `lists` nó criar o `identSize` parâmetro:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de pixels necessários para a margem de recuo.

## Configurar a altura do espaço editável {#editablespace}

>[!NOTE]
Isso só é aplicável ao usar o RTE em uma caixa de diálogo (não na edição no local na interface clássica).

É possível definir a altura do espaço editável mostrado na caixa de diálogo do componente:

1. No `../items/text` na definição da caixa de diálogo do componente, crie uma nova propriedade:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valor** a altura da tela de edição em pixels.

   >[!NOTE]
   Isso não altera a altura da janela de diálogo.

1. Salve as alterações.

## Configurar estilos e protocolos para links {#linkstyles}

Ao adicionar links em AEM, você pode definir:

* Os estilos de CSS a serem usados
* Os protocolos aceitos automaticamente

Para configurar como os links são adicionados no AEM a partir de outro programa, defina as regras de HTML.

1. Localize o componente de texto do seu projeto usando o CRXDE Lite.
1. Crie um novo nó no mesmo nível que `<rtePlugins-node>`, ou seja, crie o nó sob o nó pai de `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   O `../items/text` O nó tem a propriedade :
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`

   A localização da variável `../items/text` pode variar, dependendo da estrutura da caixa de diálogo; dois exemplos são `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Em `htmlRules`, crie um novo nó.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. Em `links` nó defina as propriedades conforme necessário:

   * Estilo CSS para links internos:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um &#39;.&#39; anterior; por exemplo, `cssClass` em vez de `.cssClass`)
   * Estilo CSS para links externos

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um &#39;.&#39; anterior; por exemplo, `cssClass` em vez de `.cssClass`)
   * Matriz válida **protocolos**. Os protocolos compatíveis são `http://`, `https://`, `file://`e `mailto:`.

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valor**(s) um ou mais protocolos
   * **defaultProtocol** (propriedade do tipo **String**): Protocolo a ser usado se o usuário não especificou um explicitamente.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valor**(s) um ou mais protocolos padrão
   * Definição de como lidar com o atributo target de um link. Crie um novo nó:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

      No nó `targetConfig`: defina as propriedades necessárias:

      * Especifique o modo de destino:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valor** s) :

            * `auto`: significa que um objetivo automático é escolhido

               (especificado pelo `targetExternal` propriedade de links externos ou `targetInternal` para links internos).

            * `manual`: não aplicável neste contexto
            * `blank`: não aplicável neste contexto
      * O target para links internos:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valor** o target para links internos (use somente quando o modo estiver `auto`)
      * O target para links externos:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valor** o target para links externos (usado somente quando o modo é `auto`).








1. Salve todas as alterações.
