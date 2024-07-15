---
title: Configurar os plug-ins do Editor de Rich Text
description: Saiba como configurar os plug-ins do Editor de Rich Text do Adobe Experience Manager para ativar funcionalidades individuais.
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '4391'
ht-degree: 2%

---


# Configurar os plug-ins do Editor de Rich Text {#configure-the-rich-text-editor-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade de recursos. É possível configurar a propriedade de recursos para ativar ou desativar um ou mais recursos de RTE. Este artigo descreve como configurar especificamente os plug-ins do RTE.

Para obter detalhes sobre as outras configurações do RTE, consulte [Configurar Rich Text Editor](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Ao trabalhar com o CRXDE Lite, é recomendável salvar as alterações regularmente usando a opção [!UICONTROL Salvar tudo].

## Ativar um plug-in e configurar a propriedade de recursos {#activateplugin}

Para ativar um plug-in, siga estas etapas. Algumas etapas são necessárias somente quando você configura um plug-in pela primeira vez, pois os nós correspondentes não existem.

Por padrão, os plug-ins `format`, `link`, `list`, `justify` e `control` e todos os seus recursos estão habilitados no RTE.

>[!NOTE]
>
>O respectivo nó `rtePlugins` é chamado de `<rtePlugins-node>` para evitar duplicação neste artigo.

1. Usando o CRXDE Lite, localize o componente de texto para o seu projeto.
1. Crie o nó pai de `<rtePlugins-node>`, se ele não existir, antes de configurar plug-ins do RTE:

   * Dependendo do componente, os nós principais são:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * um nó de configuração alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`

   * São do tipo: **jcr:primaryType** `cq:Widget`
   * Ambos têm as seguintes propriedades:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valor** `./text`

1. Dependendo da interface para a qual você está configurando, crie um nó `<rtePlugins-node>`, se ele não existir:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Abaixo disso, crie um nó para cada plug-in que você deseja ativar:

   * **Tipo** `nt:unstructured`
   * **Nome** a ID do Plug-in do plug-in necessária

Depois de ativar um plug-in, siga estas diretrizes para configurar a propriedade `features`.

| | Habilitar todos os recursos | Habilitar alguns recursos específicos | Desabilitar todos os recursos |
|---|---|---|---|
| Nome | recursos | recursos | recursos |
| Tipo | String | Cadeia de caracteres [] (cadeia múltipla; defina Tipo como Cadeia de Caracteres e clique em Múltiplo no CRXDE Lite) | String |
| Valor | `*` (um asterisco) | defina como um ou mais valores de recurso | - |

## Entender o plug-in findreplace {#findreplace}

O plug-in `findreplace` não precisa de nenhuma configuração. Funciona imediatamente.

Ao usar a funcionalidade de substituição, a cadeia de caracteres de substituição a ser substituída deve ser inserida ao mesmo tempo que a cadeia de caracteres de localização. No entanto, você ainda pode clicar em localizar para procurar a cadeia de caracteres antes de substituí-la. Se a cadeia de caracteres de substituição for inserida após clicar em localizar, a pesquisa será redefinida para o início do texto.

A caixa de diálogo localizar e substituir se torna transparente quando a localização é clicada, e se torna opaca ao clicar em substituir. Isso permite que o autor revise o texto que ele substitui. Se os usuários clicarem em substituir tudo, a caixa de diálogo será fechada e exibirá o número de substituições feitas.

## Configurar os modos de colagem {#paste-modes}

Ao usar o RTE, os autores podem colar o conteúdo em um dos três modos a seguir:

* **Modo do navegador**: cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode apresentar marcação indesejada.

* **Modo de texto sem formatação**: cole o conteúdo da área de transferência como texto sem formatação. Ele remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir no componente [!DNL Experience Manager].

* **Modo do MS® Word**: cole o texto, incluindo tabelas, com formatação ao copiar do MS® Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou o MS® Excel, e ela retém apenas formatação parcial.

### Configurar opções de Colagem disponíveis na barra de ferramentas do RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Você pode fornecer alguns, todos ou nenhum desses três ícones aos autores na barra de ferramentas do RTE:

* **[!UICONTROL Colar (Ctrl+V)]**: pode ser pré-configurado para corresponder a um dos três modos de Colagem acima.

* **[!UICONTROL Colar como Texto]**: fornece a funcionalidade de modo de texto simples.

* **[!UICONTROL Colar do Word]**: fornece a funcionalidade do modo MS® Word.

Para configurar o RTE para exibir os ícones necessários, siga estas etapas.

1. Navegue até o componente, por exemplo, `/apps/<myProject>/components/text`.
1. Navegue até o nó `rtePlugins/edit`. Consulte [ativar um plug-in](#activateplugin) se o nó não existir.
1. Crie a propriedade `features` no nó `edit` e adicione um ou mais recursos. Salve todas as alterações.

### Configurar o comportamento do ícone e do atalho Colar (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Você pode pré-configurar o comportamento do ícone **[!UICONTROL Colar (Ctrl+V)]** usando as etapas a seguir. Essa configuração também define o comportamento do atalho de teclado Ctrl+V que os autores usam para colar conteúdo.

A configuração permite os três tipos de casos de uso a seguir:

* Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode apresentar marcação indesejada. Configurado usando `browser` abaixo.

* Cole o conteúdo da área de transferência como texto simples. Ele remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir no componente AEM. Configurado usando `plaintext` abaixo.

* Cole o texto, incluindo tabelas, com formatação ao copiar do MS® Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou o MS® Excel, e ela retém apenas formatação parcial. Configurado usando `wordhtml` abaixo.

1. No componente, navegue até o nó `<rtePlugins-node>/edit`. Crie os nós, caso eles não existam. Para obter mais informações, consulte [ativar um plug-in](#activateplugin).
1. No nó `edit`, crie uma propriedade usando os seguintes detalhes:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Valor** Um dos modos de colagem necessários `browser`, `plaintext` ou `wordhtml`.

### Configurar os formatos permitidos ao colar o conteúdo {#pasteformats}

O modo colar como Microsoft-Word (`paste-wordhtml`) pode ser configurado ainda mais para que você possa definir explicitamente quais estilos são permitidos ao colar AEM de outro programa, como o Microsoft® Word.

Por exemplo, se apenas formatos e listas em negrito forem permitidos ao colar no AEM, você poderá filtrar os outros formatos. Isso é chamado de filtragem de colagem configurável, que pode ser feito para:

* [Texto](#paste-modes)
* [Links](#linkstyles)

Para links, você também pode definir os protocolos que são aceitos automaticamente.

Para configurar quais formatos são permitidos ao colar texto em AEM de outro programa:

1. No componente, navegue até o nó `<rtePlugins-node>/edit`. Crie os nós, caso eles não existam. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie um nó sob o nó `edit` para que você possa manter as regras de colagem de HTML:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Crie um nó em `htmlPasteRules` para que você possa manter os detalhes dos formatos básicos permitidos:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar os formatos individuais aceitos, crie uma ou mais das seguintes propriedades no nó `allowBasics`:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (para links e âncoras nomeadas)
   * **Nome** `image`

   Todas as propriedades são do **Tipo** `Boolean`, portanto, no **Valor** apropriado, você pode selecionar ou remover a marca de seleção para habilitar ou desabilitar a funcionalidade.

   >[!NOTE]
   >
   >Se não estiver definido explicitamente, o valor padrão true é usado e o formato é aceito.

1. Outros formatos também podem ser definidos usando um intervalo de outras propriedades ou nós, também aplicados ao nó `htmlPasteRules`. Salve todas as alterações.

Você pode usar as seguintes propriedades para `htmlPasteRules`.

| Propriedade | Tipo | Descrição |
|---|---|---|
| `allowBlockTags` | String | Define a lista de tags de bloqueio permitidas. Algumas tags de bloco possíveis incluem: <ul> <li>títulos (h1, h2, h3)</li> <li>na alínea p)</li> <li>listas (ol, ul)</li> <li>tabelas (tabela)</li> </ul> |
| `fallbackBlockTag` | String | Define a marca de bloco usada para qualquer bloco que tenha uma marca de bloco não incluída em `allowBlockTags`. `p` geralmente é suficiente. |
| tabela | nt:unstructured | Define o comportamento ao colar tabelas. Este nó deve ter a propriedade `allow` (tipo Booleano) para definir se a colagem de tabelas é permitida. Se allow estiver definido como `false`, você deverá especificar a propriedade `ignoreMode` (tipo String) para definir como o conteúdo da tabela colada será tratado. Os valores válidos para `ignoreMode` são: <ul> <li>`remove`: remove o conteúdo da tabela.</li> <li>`paragraph`: Transforma células de tabela em parágrafos.</li> </ul> |
| list | nt:unstructured | Define o comportamento ao colar listas. É necessário ter a propriedade `allow` (tipo Booleano) para definir se a colagem de listas é permitida. Se `allow` estiver definido como `false`, você deve especificar a propriedade `ignoreMode` (tipo Cadeia de Caracteres) para definir como tratar qualquer conteúdo de lista colado. Os valores válidos para `ignoreMode` são: <ul><li> `remove`: remove o conteúdo da lista.</li> <li>`paragraph`: transforma itens de lista em parágrafos.</li> </ul> |

Um exemplo de estrutura `htmlPasteRules` válida está abaixo.

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

Os autores podem aplicar Estilos para alterar a aparência de uma parte do texto. Os estilos são baseados em classes CSS que você predefine na sua folha de estilos CSS. O conteúdo estilizado está entre `span` tags usando o atributo `class` para fazer referência à classe CSS. Por exemplo, `<span class=monospaced>Monospaced Text Here</span>`.

Quando o plug-in Estilos é ativado pela primeira vez, nenhum estilo padrão está disponível. A lista pop-up está vazia. Para fornecer estilos aos autores, faça o seguinte:

* Ative o seletor suspenso Estilo.
* Especifique os locais das folhas de estilos.
* Especifique os estilos individuais que podem ser selecionados na lista suspensa Estilo.

Para configurações posteriores, digamos adicionar mais estilos, siga apenas as instruções para fazer referência a uma nova folha de estilos e especificar os estilos adicionais.

>[!NOTE]
>
>Você pode definir Estilos para [tabelas ou células de tabela](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Essas configurações exigem procedimentos separados.

### Ativar a lista suspensa de seletores Estilo {#styleselectorlist}

Isso é feito ativando o plug-in de estilo.

1. No componente, navegue até o nó `<rtePlugins-node>/styles`. Crie os nós, caso eles não existam. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a propriedade `features` no nó `styles`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Salve todas as alterações.

>[!NOTE]
>
>Quando o plug-in Estilos estiver ativado, a lista suspensa Estilo será exibida na caixa de diálogo de edição. No entanto, a lista fica vazia, pois nenhum estilo é configurado.

### Especificar o local da folha de estilos {#locationofstylesheet}

Em seguida, especifique os locais das folhas de estilos que você deseja referenciar:

1. Navegue até o nó raiz do componente de texto, por exemplo, `/apps/<myProject>/components/text`.
1. Adicionar a propriedade `externalStyleSheets` ao nó pai de `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (várias cadeias de caracteres; clique em **Várias** no CRXDE)
   * **Valores** O caminho e o nome de arquivo de cada folha de estilos que você deseja incluir. Usar caminhos do repositório.

   >[!NOTE]
   >
   >É possível adicionar referências a folhas de estilos adicionais posteriormente.

1. Salve todas as alterações.

>[!NOTE]
>
>Ao usar o RTE em uma caixa de diálogo (interface clássica), talvez você queira especificar folhas de estilos otimizadas para edição de rich text. Devido a restrições técnicas, o contexto CSS é perdido no editor, portanto, convém emular esse contexto para melhorar a experiência WYSIWYG.
>
>O Editor de Rich Text usa um elemento DOM de contêiner com uma ID de `CQrte` que pode ser usada para fornecer estilos diferentes para exibição e edição:
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### Especificar os estilos disponíveis na lista pop-up {#stylesindropdown}

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/styles`, conforme criado em [Habilitando o seletor suspenso de estilos](#styleselectorlist).
1. No nó `styles`, crie um nó (também chamado `styles`) para manter a lista que está sendo disponibilizada:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó sob o nó `styles` para que você possa representar um estilo individual:

   * **Nome**, você pode especificar o nome, mas ele deve ser adequado para o estilo
   * **Tipo** `nt:unstructured`

1. Adicione a propriedade `cssName` a este nó para que você possa fazer referência à classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valor** O nome da classe CSS (sem um &#39;.&#39; precedente; por exemplo, `cssClass` em vez de `.cssClass`)

1. Adicione a propriedade `text` ao mesmo nó; isso define o texto mostrado na caixa de seleção:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valor** Descrição do estilo; aparece na caixa de seleção suspensa Estilo.

1. Salve as alterações.

   Repita as etapas acima para cada estilo necessário.

### Configurar o RTE para quebras de palavras ideais em japonês {#jpwordwrap}

Os autores que usam AEM para criar conteúdo no idioma japonês podem aplicar um estilo aos caracteres para evitar quebras de linha, quando uma quebra não é necessária. Isso permite que os autores deixem as frases serem quebradas na posição desejada. O estilo dessa funcionalidade é baseado na classe CSS, que é predefinida na folha de estilos CSS.

>[!NOTE]
>
>Esse recurso exige pelo menos o AEM 6.5 Service Pack 1.

Para criar o estilo que os autores podem aplicar ao texto em japonês, siga estas etapas:

1. Crie um nó sob o nó estilos. Consulte [especificar um novo estilo](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Adicione a propriedade `cssName` ao nó para que você possa fazer referência à classe CSS. Este nome de classe é um nome reservado para o recurso de quebra de linha em japonês.
   * Nome: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sem um `.` precedente)

1. Adicione o texto da propriedade ao mesmo nó. O valor é o nome do estilo que o autor vê ao selecionar o estilo.
   * Nome: `text`
*Tipo: `String`
   * Valor: `Japanese word-wrap`

1. Crie uma folha de estilos e especifique seu caminho. Consulte [especificar local da folha de estilos](#locationofstylesheet). Adicione o conteúdo a seguir à folha de estilos. Altere a cor do plano de fundo conforme desejado.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Folha de estilos para disponibilizar o recurso de quebra automática de linha em japonês para os autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurar os formatos de parágrafo {#paraformats}

Qualquer texto criado no RTE é colocado em uma marca de bloco, sendo o padrão `<p>`. Ao habilitar o plug-in `paraformat`, você especifica marcas de formatação de bloco adicionais que podem ser atribuídas a parágrafos, usando uma lista suspensa de seleção. Os formatos de parágrafo determinam o tipo de parágrafo atribuindo a marca de formatação de bloco correta. O autor pode selecioná-los e atribuí-los usando o seletor de Formato. As tags de bloco de exemplo incluem, entre outros, o parágrafo padrão &lt;p> e os cabeçalhos &lt;h1>, &lt;h2>, entre outros.

>[!CAUTION]
>
>Esse plug-in não é adequado para conteúdo com estruturas complexas, como listas ou tabelas.

>[!NOTE]
>
>Se uma tag de bloco, por exemplo, uma tag &lt;hr>, não puder ser atribuída a um parágrafo, isso não será um caso de uso válido para um plug-in paraformat.

Quando o plug-in Formatos de parágrafo é ativado pela primeira vez, nenhum Formato de parágrafo padrão está disponível. A lista pop-up está vazia. Para fornecer aos autores os Formatos de parágrafo, faça o seguinte:

* Habilite a lista suspensa de seletores Formato.
* Especifique as tags de bloco que podem ser selecionadas como formatos de parágrafo no menu suspenso.

Para configurações ou reconfigurações posteriores, diga para adicionar mais formatos, siga apenas a parte relevante das instruções.

### Ativar o seletor suspenso Formatar {#formatselectorlist}

Primeiro, ative o plug-in paraformat:

1. No componente, navegue até o nó `<rtePlugins-node>/paraformat`. Crie os nós, caso eles não existam. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a propriedade `features` no nó `paraformat`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
Se o plug-in não for configurado ainda mais, os seguintes formatos padrão serão ativados:
>
* Parágrafo ( `<p>`)
* Título 1 ( `<h1>`)
* Título 2 ( `<h2>`)
* Título 3 ( `<h3>`)
>

>[!CAUTION]
>
Ao configurar o formato de parágrafo do RTE, não remova a tag de parágrafo &lt;p> como uma opção de formatação. Se a marca `<p>` for removida, o autor de conteúdo não poderá selecionar a opção **Formatos de parágrafo**, mesmo se houver formatos adicionais configurados.

### Especificar os formatos de parágrafo disponíveis {#paraformatsindropdown}

Os formatos de parágrafo podem ser disponibilizados para seleção por:

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/paraformat`, conforme criado em [Habilitando o seletor suspenso de formato](#styleselectorlist).
1. No nó `paraformat`, crie um nó para conter a lista de formatos:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó sob o nó `formats`, isso contém detalhes para um formato individual:

   * **Nome**, você pode especificar o nome, mas ele deve ser adequado para o formato (por exemplo, myParagraph, myheader1).
   * **Tipo** `nt:unstructured`

1. Neste nó, adicione a propriedade para definir a tag de bloqueio usada:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valor** A marca de bloco para o formato; por exemplo: p, h1, h2.

     Não é necessário inserir os colchetes angulares delimitadores.

1. Para o mesmo nó, adicione outra propriedade para que o texto descritivo apareça na lista suspensa:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valor** O texto descritivo para este formato; por exemplo, Parágrafo, Cabeçalho 1, Cabeçalho 2. Esse texto é exibido na lista de seleção de Formato.

1. Salve as alterações.

   Repita as etapas para cada formato necessário.

>[!CAUTION]
>
Se você definir formatos personalizados, os formatos padrão (`<p>`, `<h1>`, `<h2>` e `<h3>`) serão removidos. Recrie o formato `<p>`, pois ele é o formato padrão.

## Configurar caracteres especiais {#spchar}

Em uma instalação padrão do AEM, quando o plug-in `misctools` é habilitado para caracteres especiais (`specialchars`), uma seleção padrão é imediatamente disponibilizada para uso; por exemplo, os símbolos de copyright e marca comercial.

É possível configurar o RTE para disponibilizar sua própria seleção de caracteres; definindo caracteres distintos ou uma sequência inteira.

>[!CAUTION]
>
Adicionar seus próprios caracteres especiais substitui a seleção padrão. Se necessário, defina ou redefina esses caracteres em sua própria seleção.

### Definir um caractere único {#definesinglechar}

1. No componente, navegue até o nó `<rtePlugins-node>/misctools`. Crie os nós, caso eles não existam. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a propriedade `features` no nó `misctools`:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

         (ou `String / *` se estiver aplicando todos os recursos deste plug-in)

1. Em `misctools`, crie um nó para conter as configurações de caracteres especiais:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. Em `specialCharsConfig`, crie outro nó para conter a lista de caracteres:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. Em `chars`, adicione um nó para conter uma definição de caractere individual:

   * **Nome** você pode especificar o nome, mas ele deve refletir o caractere; por exemplo, metade.
   * **Tipo** `nt:unstructured`

1. Neste nó, adicione a seguinte propriedade:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Value** a representação de HTML do caractere necessário; por exemplo, `&189;` para a fração metade.

1. Salve as alterações.

No CRXDE, depois que a propriedade é salva, o caractere representado é exibido. Veja abaixo o exemplo de metade. Repita as etapas acima para que você possa disponibilizar mais caracteres especiais aos autores.

![No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE](assets/chlimage_1-106.png "No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE")

### Definir um intervalo de caracteres {#definerangechar}

1. Use as etapas 1 a 3 de [Definindo um Único Caractere](#definesinglechar).
1. Em `chars`, adicione um nó para conter a definição do intervalo de caracteres:

   * **Nome** você pode especificar o nome, mas ele deve refletir o intervalo de caracteres; por exemplo, lápis.
   * **Tipo** `nt:unstructured`

1. Nesse nó (nomeado de acordo com o intervalo de caracteres especiais), adicione as duas propriedades a seguir:

   * **Nome** `rangeStart`
     **Tipo** `Long`
     **Value** a representação [Unicode](https://unicode.org/) (decimal) do primeiro caractere no intervalo

   * **Nome** `rangeEnd`
     **Tipo** `Long`
     **Valor** a representação (decimal) [Unicode](https://unicode.org/) do último caractere no intervalo

1. Salve as alterações.

   Por exemplo, definir um intervalo de 9998 a 10000 fornece os seguintes caracteres.

   ![No CRXDE, defina um intervalo de caracteres a serem disponibilizados no RTE](assets/chlimage_1-107.png)

   *Figura: no CRXDE, defina um intervalo de caracteres a ser disponibilizado no RTE*

   ![Os caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up](assets/rtepencil.png "Os caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up")

## Configurar estilos de tabela {#tablestyles}

Normalmente, os estilos são aplicados em texto, mas um conjunto separado de estilos também pode ser aplicado a uma tabela ou a algumas células da tabela. Esses Estilos estão disponíveis para os autores na caixa do seletor de estilo na caixa de diálogo Propriedades da célula ou Propriedades da tabela. Os estilos estão disponíveis ao editar uma tabela em um componente de Texto (ou derivativo) e não no componente de Tabela padrão.

>[!NOTE]
>
É possível definir estilos para tabelas e células somente para a interface clássica.

>[!NOTE]
>
Copiar e colar tabelas no componente de RTE ou a partir dele depende do navegador. Ele não é compatível imediatamente com todos os navegadores. É possível obter resultados variados dependendo da estrutura da tabela e do navegador. Por exemplo, ao copiar e colar uma tabela em um componente do RTE no Mozilla Firefox na interface clássica e na interface para toque, o layout da tabela não é preservado.

1. No componente, navegue até o nó `<rtePlugins-node>/table`. Crie os nós, caso eles não existam. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a propriedade `features` no nó `table`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

   >[!NOTE]
   >
   Se você não quiser habilitar todos os recursos de tabela, poderá criar a propriedade `features` como:
   >
   * **Tipo** `String[]`
   >
   * **Valor** um ou ambos, conforme necessário:
   * `table` para permitir a edição das propriedades da tabela; incluindo os estilos.
   * `cellprops` para permitir a edição das propriedades da célula, incluindo os estilos.

1. Defina o local das folhas de estilos CSS para que você possa referenciá-las. Consulte [Especificar o local da folha de estilos](#locationofstylesheet), pois é o mesmo que ao definir [estilos para texto](#textstyles). O local pode ser definido se você tiver definido outros estilos.
1. No nó `table`, crie os seguintes nós novos (conforme necessário):

   * Para definir estilos para a tabela inteira (disponível em **Propriedades da tabela**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`

   * Para definir estilos para as células individuais (disponível em **Propriedades da célula**):

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`

1. Crie um nó (sob o nó `tableStyles` ou `cellStyles`, conforme apropriado) para que possa representar um estilo individual:

   * **Nome** você pode especificar o nome, mas ele deve refletir o estilo.
   * **Tipo** `nt:unstructured`

1. Neste nó, crie as propriedades:

   * Para definir o estilo CSS a ser referenciado

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Value** o nome da classe CSS (sem um `.` precedente, por exemplo, `cssClass` em vez de `.cssClass`)

   * Para definir que um texto descritivo seja exibido no seletor suspenso

      * **Nome** `text`
      * **Tipo** `String`
      * **Valor** o texto a ser exibido na lista de seleção

1. Salve todas as alterações.

Repita as etapas acima para cada estilo necessário.

### Configurar cabeçalhos ocultos em tabelas para acessibilidade {#hiddenheader}

Às vezes, você pode criar tabelas de dados sem texto visual em um cabeçalho de coluna, supondo que a finalidade do cabeçalho esteja implícita no relacionamento visual da coluna com outras colunas. Nesse caso, é necessário fornecer texto interno oculto dentro da célula na célula de cabeçalho. Dessa forma, leitores de tela e outras tecnologias de assistência podem ajudar os leitores com várias necessidades a entender o propósito da coluna.

Para aprimorar a acessibilidade em tais cenários, o RTE oferece suporte a células de cabeçalho ocultas. Além disso, fornece definições de configuração relacionadas a cabeçalhos ocultos em tabelas. Essas configurações permitem aplicar estilos de CSS a cabeçalhos ocultos nos modos de edição e pré-visualização. Para ajudar os autores a identificar cabeçalhos ocultos no modo de edição, inclua os seguintes parâmetros no código:

* `hiddenHeaderEditingCSS`: especifica o nome da classe CSS aplicada na célula de cabeçalho oculto, quando o RTE é editado.
* `hiddenHeaderEditingStyle`: especifica uma cadeia de caracteres de Estilo que é aplicada na célula de cabeçalho oculto quando o RTE é editado.

Se você especificar o CSS e a string de estilo no código, a classe CSS terá prioridade sobre a string de estilo e poderá substituir quaisquer alterações de configuração feitas pela string de estilo.

Para ajudar os autores a aplicarem o CSS em cabeçalhos ocultos no modo de visualização, você pode incluir os seguintes parâmetros no código:

* `hiddenHeaderClassName`: especifica o nome da classe CSS aplicada na célula de cabeçalho oculta no modo de visualização.
* `hiddenHeaderStyle`: especifica uma cadeia de caracteres de Estilo que é aplicada na célula de cabeçalho oculto no modo de visualização.

Se você especificar o CSS e a string de estilo no código, a classe CSS terá prioridade sobre a string de estilo e poderá substituir quaisquer alterações de configuração feitas pela string de estilo.

## Adicionar dicionários para o verificador ortográfico {#adddict}

Quando o plug-in de verificação ortográfica é ativado, o RTE usa dicionários para cada idioma apropriado. Eles são selecionados de acordo com o idioma do site, pegando a propriedade language da subárvore ou extraindo o idioma do URL. Por exemplo, a ramificação `/en/` é marcada como inglês, a ramificação `/de/` como alemão.

>[!NOTE]
>
A mensagem `Spell checking failed` será vista se for tentada uma verificação para um idioma que não está instalado. Os dicionários padrão estão em `/libs/cq/spellchecker/dictionaries`, junto com os arquivos readme apropriados. Não modifique os arquivos.

Uma instalação padrão do AEM inclui os dicionários inglês americano (`en_us`) e inglês britânico (`en_gb`). Para adicionar mais dicionários, siga estas etapas.

1. Navegue até a página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Siga um destes procedimentos para localizar um dicionário de sua escolha de idioma:

   * Procure o dicionário de sua escolha de idioma. Na página do dicionário, localize o link para a fonte original ou página da Web do autor. Localize os arquivos do dicionário para a v2.x nessa página.
   * Procurar arquivos do dicionário v2.x em [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Baixe o arquivo com as definições de ortografia. Extraia o conteúdo do arquivo morto em seu sistema de arquivos.

   >[!CAUTION]
   >
   Somente dicionários no formato `MySpell` para OpenOffice.org v2.0.1 ou anterior são suportados. Como os dicionários agora são arquivos mortos, é recomendável verificar o arquivo após baixá-lo.

1. Localize os arquivos `.aff` e `.dic`. Mantenha o nome do arquivo em minúsculas. Por exemplo, `de_de.aff` e `de_de.dic`.
1. Carregar os arquivos `.aff` e `.dic` no repositório em `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
O verificador ortográfico RTE está disponível sob demanda. Ele não é executado automaticamente quando você começa a digitar o texto. Para executar o verificador ortográfico, clique em [!UICONTROL Verificador ortográfico] na barra de ferramentas. O RTE verifica a ortografia das palavras e destaca as palavras com erro de ortografia.
>
Se você incorporar qualquer alteração sugerida pelo verificador ortográfico, o estado do texto será alterado e as palavras com erro de ortografia não serão mais destacadas. Para executar o verificador ortográfico, clique novamente no botão Verificador ortográfico.

## Configurar o tamanho do histórico das ações desfazer e refazer {#undohistory}

O RTE permite que os autores desfaçam ou refaçam algumas últimas edições. Por padrão, 50 edições são armazenadas no histórico. Você pode configurar esse valor conforme necessário.

1. No componente, navegue até o nó `<rtePlugins-node>/undo`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No nó `undo`, crie a propriedade:

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Value** o número de etapas de desfazer que você deseja salvar no histórico. O padrão é 50. Use `0` para desabilitar completamente desfazer/refazer.

1. Salve as alterações.

## Configurar o tamanho da guia {#tabsize}

Quando o caractere de tabulação é pressionado dentro de qualquer texto, um número predefinido de espaços é inserido; por padrão, são três espaços não-separáveis e um espaço.

Para definir o tamanho da guia:

1. No componente, navegue até o nó `<rtePlugins-node>/keys`. Crie os nós, caso eles não existam. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No nó `keys`, crie a propriedade:

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valor** o número de caracteres de espaço a serem usados para a tabulação

1. Salve as alterações.

## Definir margem de recuo {#indentmargin}

Quando o recuo está ativado (padrão), você pode definir o tamanho do recuo:

>[!NOTE]
>
Este tamanho de recuo é aplicado somente a parágrafos (blocos) de texto; não afeta o recuo de listas reais.

1. No componente, navegue até o nó `<rtePlugins-node>/lists`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No nó `lists`, crie o parâmetro `indentSize`:

   * **Nome**: `indentSize`
   * **Tipo**: `Long`
   * **Valor**: número de pixels necessários para a margem de recuo.

## Configurar a altura do espaço editável {#editablespace}

>[!NOTE]
>
Isso só é aplicável ao usar o RTE em uma caixa de diálogo (não na edição no local na interface clássica).

Você pode definir a altura do espaço editável mostrado na caixa de diálogo do componente:

1. No nó `../items/text`, na definição da caixa de diálogo do componente, crie uma propriedade:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valor** a altura da tela de edição em pixels.

   >[!NOTE]
   >
   Isso não altera a altura da janela de diálogo.

1. Salve as alterações.

## Configurar estilos e protocolos para links {#linkstyles}

Ao adicionar links no AEM, é possível definir:

* Os estilos de CSS a serem usados
* Os protocolos aceitos automaticamente

Para configurar como os links são adicionados no AEM de outro programa, defina as regras de HTML.

1. Usando o CRXDE Lite, localize o componente de texto para o seu projeto.
1. Crie um nó no mesmo nível que `<rtePlugins-node>`, ou seja, crie o nó sob o nó pai de `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   >
   O nó `../items/text` tem a propriedade:
   >
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`
   >
   O local do nó `../items/text` pode variar, dependendo da estrutura da caixa de diálogo. Dois exemplos são `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Em `htmlRules`, crie um nó.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. No nó `links`, defina as propriedades conforme necessário:

   * Estilo CSS para links internos:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Value** o nome da classe CSS (sem um &#39;.&#39; precedente; por exemplo, `cssClass` em vez de `.cssClass`)

   * Estilo CSS para links externos

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Value** o nome da classe CSS (sem um &#39;.&#39; precedente; por exemplo, `cssClass` em vez de `.cssClass`)

   * Matriz de **protocolos** válidos. Os protocolos com suporte são `http://`, `https://`, `file://` e `mailto:`.

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valor** um ou mais protocolos

   * **defaultProtocol** (propriedade do tipo **String**): protocolo a ser usado se o usuário não tiver especificado explicitamente um.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valor** um ou mais protocolos padrão

   * Definição de como lidar com o atributo de direcionamento de um link. Criar um nó:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

     No nó `targetConfig`, defina as propriedades necessárias:

      * Especifique o modo de destino:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valor**

            * `auto`: significa que um destino automático foi escolhido

              (especificado pela propriedade `targetExternal` para links externos ou `targetInternal` para links internos).

            * `manual`: não aplicável neste contexto
            * `blank`: não aplicável neste contexto

      * O target para links internos:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Value** o destino para links internos (use somente quando o modo for `auto`)

      * O target para links externos:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Value** o destino para links externos (usado apenas quando o modo é `auto`).

1. Salve todas as alterações.
