---
title: Andaime
description: Às vezes, pode ser necessário criar um grande conjunto de páginas que compartilha a mesma estrutura, mas tem um conteúdo diferente. Com o scaffolding, você pode criar um formulário (um scaffold) com os campos que refletem a estrutura desejada para suas páginas e usar esse formulário para criar facilmente páginas com base nessa estrutura.
uuid: 5904abc0-b256-4da4-a7d7-3c17ea299648
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: a63e5732-b1a3-4639-9838-652af401e788
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 0%

---

# Andaime{#scaffolding}

Às vezes, pode ser necessário criar um grande conjunto de páginas que compartilha a mesma estrutura, mas tem um conteúdo diferente. Por meio da interface de AEM padrão, seria necessário criar cada página, arrastar os componentes apropriados para a página e preencher cada um deles individualmente.

Com o scaffolding, você pode criar um formulário (um scaffold) com os campos que refletem a estrutura desejada para suas páginas e usar esse formulário para criar facilmente páginas com base nessa estrutura.

>[!NOTE]
>
>Andaime (na interface clássica) [respeita a herança MSM](#scaffolding-with-msm-inheritance).

## Como o scaffolding funciona {#how-scaffolding-works}

Os scaffolds são armazenados no **Ferramentas** do administrador do site.

* Abra o **Ferramentas** e clique em **Andaime de página padrão**.
* Em seguida, clique em **geometrixx**.
* Em **geometrixx** você encontrará um *página de scaffold* chamado **Notícias**. Clique duas vezes para abrir esta página.

![howscaffolds_work](assets/howscaffolds_work.png)

O scaffold consiste em um formulário com um campo para cada parte de conteúdo que compõe a página a ser criada e quatro parâmetros importantes que são acessados por meio da variável **Propriedades da página** da página de scaffold.

![pageprops](assets/pageprops.png)

As propriedades da página de scaffolding são:

* **Texto do título**: Este é o nome desta própria página de scaffolding. Neste exemplo, chama-se &quot;Notícias&quot;.
* **Descrição**: Isso é exibido abaixo do título na página de scaffolding.
* **Modelo de destino**: Esse é o modelo que o scaffold usará ao criar uma nova página. Neste exemplo, é um *Página Conteúdo Geometrrixx* modelo .
* **Caminho do Target**: Esse é o caminho da página pai abaixo da qual esse scaffold criará novas páginas. Neste exemplo, o caminho é */content/geometrixx/en/news*.

O corpo do scaffold é o formulário. Quando um usuário deseja criar uma página usando o scaffold, ele preenche o formulário e clica em *Criar*, na parte inferior. No **Notícias** O exemplo acima do formulário tem os seguintes campos:

* **Título**: Esse é o nome da página a ser criada. Este campo está sempre presente em cada scaffold.
* **Texto**: Esse campo corresponde a um Componente de texto na página resultante.
* **Imagem**: Esse campo corresponde a um Componente de imagem na página resultante.
* **Imagem/avançado**: **Título**: O título da imagem.
* **Imagem/avançado**: **Texto alternativo**: O texto alternativo da imagem.
* **Imagem/avançado**: **Descrição**: A descrição da imagem.
* **Imagem/avançado**: **Tamanho**: O tamanho da imagem.
* **Tags/Palavras-chave**: Metadados a serem atribuídos a esta página. Este campo está sempre presente em cada scaffold.

### Criação de um scaffold {#creating-a-scaffold}

Para criar um novo scaffold, acesse **Ferramentas** , em seguida **Andaime de página padrão** e criar uma nova página. Um tipo de modelo de página única estará disponível, a variável *Modelo de scaffolding.*

Vá para o **Propriedades da página** da nova página e defina a variável *Texto do título*, *Descrição*, *Modelo de destino* e *Caminho do Target*, conforme descrito acima.

Em seguida, é necessário definir a estrutura da página que esse scaffold criará. Para fazer isso, acesse **[modo de design](/help/sites-authoring/page-authoring.md#sidekick)** na página de scaffold. Um link será exibido permitindo que você edite o scaffold no **editor de caixas de diálogo**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

Usando o editor de caixas de diálogo, especifique as propriedades que serão criadas sempre que uma nova página for criada usando esse scaffold.

A definição da caixa de diálogo para um scaffold funciona de maneira semelhante à de um componente (consulte [Componentes](/help/sites-developing/components.md)). No entanto, algumas diferenças importantes se aplicam:

* As definições da caixa de diálogo do componente são renderizadas como caixas de diálogo normais (como mostrado no painel médio do editor de caixa de diálogo, por exemplo) enquanto as definições da caixa de diálogo de scaffold, embora sejam exibidas como caixas de diálogo normais no editor de caixas de diálogo, são renderizadas na página de scaffold como um formulário de scaffold (como mostrado no **Notícias** scaffold acima).
* As caixas de diálogo de componente fornecem campos apenas para os valores necessários para definir o conteúdo de um único componente específico. Uma caixa de diálogo de scaffold deve fornecer campos para cada propriedade em cada parágrafo da página a ser criada.
* No caso de caixas de diálogo de componentes, o componente usado para renderizar o conteúdo especificado é implícito e, portanto, o `sling:resourceType` a propriedade do parágrafo é preenchida automaticamente quando o parágrafo é criado. Com um scaffold, todas as informações que definem o conteúdo e o componente atribuído para um determinado parágrafo devem ser fornecidas pela própria caixa de diálogo. Nas caixas de diálogo de scaffold, essas informações devem ser fornecidas usando *Oculto* para enviar essas informações na criação da página.

Uma análise do exemplo **Notícias** a caixa de diálogo de scaffold no editor de caixas de diálogo ajuda a explicar como isso funciona. Entre no modo de design na página de scaffold e clique no link do editor de caixas de diálogo.

Agora, clique no campo de diálogo **Caixa de diálogo > Painel de guias > Texto > Texto** assim:

![textedit](assets/textedit.png)

A lista de propriedades desse campo será exibida no lado direito do editor de caixas de diálogo, desta forma:

![list_of_properties](assets/list_of_properties.png)

Observe a propriedade name desse campo. Ela tem o valor

`./jcr:content/par/text/text`

Esse é o nome da propriedade na qual o conteúdo desse campo será gravado quando o scaffold for usado para criar uma página. A propriedade é declarada como um caminho relativo do nó que representa a página a ser criada. Especifica o texto da propriedade, abaixo do texto do nó, que está abaixo do par de nós, que é ele próprio um filho do nó jcr:content abaixo do nó da página.

Isso define o local do armazenamento de conteúdo para o texto que será inserido neste campo. No entanto, também precisamos especificar mais duas características para esse conteúdo:

* O fato de que a sequência de caracteres que está sendo armazenada aqui deve ser interpretada como *rich text* e
* qual componente deve ser usado para renderizar esse conteúdo na página resultante.

Observe que, em uma caixa de diálogo de componente normal, não seria necessário especificar essas informações porque estão implícitas no fato de a caixa de diálogo já estar vinculada a um componente específico.

Para especificar essas duas informações, use campos ocultos. Clique no primeiro campo oculto **Caixa de diálogo > Painel de guias > Texto > Oculto** assim:

![oculto](assets/hidden.png)

As propriedades desse campo oculto são as seguintes:

![hidden_list_props](assets/hidden_list_props.png)

A propriedade name desse campo oculto é

`./jcr:content/par/text/textIsRich`

Esta é uma propriedade booleana usada para interpretar a string de texto armazenada em `./jcr:content/par/text/text`.

Como sabemos que o texto deve ser interpretado como rich text, especificamos o valor `value` propriedade deste campo como `true`.

>[!CAUTION]
>
>O editor de caixas de diálogo permite que o usuário altere os valores de *existente* na definição da caixa de diálogo. Para adicionar uma nova propriedade, o usuário deve usar [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por exemplo, quando um novo campo oculto é adicionado a uma definição de caixa de diálogo com o editor de caixa de diálogo, ele não tem um *value* (ou seja, uma propriedade com o nome &quot;valor&quot;). Se o campo oculto em questão exigir um padrão *value* a ser definida, essa propriedade deve ser adicionada manualmente com uma das ferramentas do CRX. O valor não pode ser adicionado com o próprio editor de caixas de diálogo. No entanto, uma vez que a propriedade esteja presente, seu valor poderá ser editado com o editor de caixas de diálogo.

O segundo campo oculto pode ser visualizado ao clicar nele da seguinte maneira:

![hidden2](assets/hidden2.png)

As propriedades desse campo oculto são as seguintes:

![hidden_list_props2](assets/hidden_list_props2.png)

A propriedade name desse campo oculto é

`./jcr:content/par/text/sling:resourceType`

e o valor fixo especificado para esta propriedade é

`foundation/components/textimage`

Isso especifica que o componente a ser usado para renderizar o conteúdo de texto deste parágrafo é o *Imagem de texto* componente. Usar com o `isRichText` booleano especificado no outro campo oculto, o componente pode renderizar a cadeia de caracteres de texto real armazenada em `./jcr:content/par/text/text` da forma desejada.

### Andaime com herança MSM {#scaffolding-with-msm-inheritance}

Na interface clássica, o scaffolding é totalmente integrado com herança MSM (quando aplicável).

Ao abrir uma página em **Andaime** modo (usando o ícone na parte inferior do sidekick) qualquer componente sujeito à herança será indicado por:

* Um símbolo de cadeado (para a maioria dos componentes); por exemplo, Texto e Título)
* uma máscara com o texto **Clique para cancelar a herança** (para componentes de imagem)

Eles mostram que o componente não pode ser editado até que a herança seja cancelada.

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>Isso é comparável ao [componentes herdados ao editar o conteúdo da página](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Clicar no símbolo de cadeado ou no ícone de imagem permite interromper a herança:

* o símbolo será alterado para um cadeado aberto.
* depois de desbloqueado, você pode editar o conteúdo.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

Após desbloquear, é possível restaurar a herança clicando no símbolo de cadeado desbloqueado. Isso perderá todas as edições feitas.

>[!NOTE]
>
>Se a herança for cancelada no nível da página (na guia Livecopy das Propriedades da página), todos os componentes poderão ser editados em **Andaime** (serão exibidos no estado desbloqueado).
