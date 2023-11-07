---
title: Andaime
description: Às vezes, pode ser necessário criar um grande conjunto de páginas que compartilham estrutura, mas têm conteúdo diferente. Com o andaime, você pode criar um formulário (um andaime) com campos que refletem a estrutura desejada para as páginas e, em seguida, usar este formulário para criar facilmente páginas com base nessa estrutura.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 0%

---

# Andaime{#scaffolding}

Às vezes, pode ser necessário criar um grande conjunto de páginas que compartilham estrutura, mas têm conteúdo diferente. Por meio da interface padrão do Adobe Experience Manager (AEM), seria necessário criar cada página, arrastar os componentes apropriados para a página e preencher cada um deles individualmente.

Com o andaime, você pode criar um formulário (um andaime) com campos que refletem a estrutura desejada para as páginas e, em seguida, usar este formulário para criar facilmente páginas com base nessa estrutura.

>[!NOTE]
>
>Andaime (na interface clássica) [respeita a herança do MSM](#scaffolding-with-msm-inheritance).

## Como funciona o andaime {#how-scaffolding-works}

Os andaimes são armazenados no **Ferramentas** console do administrador do site.

* Abra o **Ferramentas** e clique em **Scaffolding da página padrão**.
* Nessa, clique em **Geometrixx**.
* Em **Geometrixx**, você encontrará um *página de andaime* chamado **Notícias**. Clique duas vezes para abrir esta página.

![howscaffolds_work](assets/howscaffolds_work.png)

O scaffolding consiste em um formulário com um campo para cada parte do conteúdo que irá compor a página a ser criada e quatro parâmetros importantes que são acessados por meio do **Propriedades da página** da página de andaime.

![pageprops](assets/pageprops.png)

As propriedades da página de andaime são:

* **Texto do título**: este é o nome da própria página de andaime. Neste exemplo, ele é chamado de &quot;Notícias&quot;.
* **Descrição**: Isso aparece abaixo do título na página de andaimes.
* **Modelo de destino**: este é o modelo que esse scaffolding usará ao criar uma página. Neste exemplo, é um *Página de conteúdo do Geometrixx* modelo.
* **Caminho de destino**: este é o caminho da página principal abaixo da qual este scaffolding criará páginas. Neste exemplo, o caminho é */content/geometrixx/en/news*.

O corpo do andaime é a forma. Quando um usuário deseja criar uma página usando o andaime, ele preenche o formulário e clica em *Criar*, na parte inferior. No **Notícias** exemplo acima o formulário tem os seguintes campos:

* **Título**: este é o nome da página que será criada. Este campo está sempre presente em todos os andaimes.
* **Texto**: este campo corresponde a um Componente de Texto na página resultante.
* **Imagem**: este campo corresponde a um Componente de imagem na página resultante.
* **Imagem/Avançado**: **Título**: o título da imagem.
* **Imagem/Avançado**: **Texto Alternativo**: o texto alternativo da imagem.
* **Imagem/Avançado**: **Descrição**: a descrição da imagem.
* **Imagem/Avançado**: **Tamanho**: o tamanho da imagem.
* **Tags/Palavras-chave**: metadados a serem atribuídos a esta página. Este campo está sempre presente em todos os andaimes.

### Criação de um scaffold {#creating-a-scaffold}

Para criar um scaffold, vá para a **Ferramentas** console, depois **Scaffolding da página padrão** e crie uma página. Um tipo de modelo de página única está disponível, o *Modelo de andaime.*

Vá para a **Propriedades da página** da nova página e defina o *Texto do título*, *Descrição*, *Modelo de destino*, e *Caminho de destino*, conforme descrito acima.

Em seguida, é necessário definir a estrutura da página que esse scaffolding criará. Para fazer isso, acesse **[modo de design](/help/sites-authoring/page-authoring.md#sidekick)** na página de andaime. Um link é exibido, permitindo que você edite o scaffolding no **editor de diálogo**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

Usando o editor de caixa de diálogo, especifique as propriedades que serão criadas sempre que uma nova página for criada usando esse scaffolding.

A definição da caixa de diálogo de um scaffold funciona de forma semelhante à de um componente (consulte [Componentes](/help/sites-developing/components.md)). No entanto, algumas diferenças importantes se aplicam:

* As definições de diálogo de componente são renderizadas como caixas de diálogo normais (como mostrado no painel central do editor de diálogo, por exemplo), enquanto as definições de diálogo de scaffold, embora apareçam como caixas de diálogo normais no editor de diálogo, são renderizadas na página de scaffold como um formulário de scaffold (como mostrado no **Notícias** andaime acima).
* As caixas de diálogo do componente fornecem campos apenas para os valores necessários para definir o conteúdo de um único componente específico. Uma caixa de diálogo de scaffold deve fornecer campos para cada propriedade em cada parágrafo da página que será criada.
* No caso de caixas de diálogo de componente, o componente usado para renderizar o conteúdo especificado é implícito e, portanto, o `sling:resourceType` A propriedade do parágrafo é preenchida automaticamente quando o parágrafo é criado. Com um scaffolding, todas as informações que definem o conteúdo e o componente atribuído para um determinado parágrafo devem ser fornecidas pela própria caixa de diálogo. Nas caixas de diálogo de scaffold, essas informações devem ser fornecidas usando *Oculto* para enviar essas informações sobre a criação da página.

Veja o exemplo **Notícias** a caixa de diálogo scaffold no editor de diálogo ajuda a explicar como isso funciona. Vá para o modo de design na página do andaime e clique no link do editor de diálogo.

Agora, clique no campo de diálogo **Caixa de diálogo > Painel de guias > Texto > Texto**, desta forma:

![textedit](assets/textedit.png)

A lista de propriedades desse campo aparece no lado direito do editor da caixa de diálogo, desta forma:

![list_of_properties](assets/list_of_properties.png)

Observe a propriedade de nome desse campo. Tem o valor

`./jcr:content/par/text/text`

Esse é o nome da propriedade na qual o conteúdo desse campo será escrito quando o scaffold for usado para criar uma página. A propriedade é declarada como um caminho relativo do nó que representa a página que será criada. Especifica o texto da propriedade, abaixo do texto do nó, que está abaixo do par do nó, que é ele mesmo filho do nó jcr:content abaixo do nó da página.

Isso define o local do armazenamento de conteúdo para o texto que será inserido nesse campo. No entanto, também precisamos especificar mais duas características para esse conteúdo:

* O fato de a cadeia de caracteres aqui armazenada dever ser interpretado *rich text*, e
* qual componente deve ser usado para renderizar esse conteúdo para a página resultante.

Em uma caixa de diálogo de componente normal, não seria necessário especificar essas informações, pois estão implícitas no fato de que a caixa de diálogo já está vinculada a um componente específico.

Para especificar essas duas informações, use campos ocultos. Clique no primeiro campo oculto **Caixa de diálogo > Painel de guias > Texto > Oculto**, desta forma:

![oculto](assets/hidden.png)

As propriedades desse campo oculto são as seguintes:

![hidden_list_props](assets/hidden_list_props.png)

A propriedade de nome deste campo oculto é

`./jcr:content/par/text/textIsRich`

Esta é uma propriedade booleana usada para interpretar a sequência de texto armazenada em `./jcr:content/par/text/text`.

Como sabemos que o texto deve ser interpretado como um rich text, vamos especificar o `value` propriedade deste campo como `true`.

>[!CAUTION]
>
>O editor de caixa de diálogo permite que o usuário altere os valores de *existente* propriedades na definição da caixa de diálogo. Para adicionar uma nova propriedade, o usuário deve usar [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por exemplo, quando um novo campo oculto é adicionado a uma definição de caixa de diálogo com o editor de caixa de diálogo, ele não tem uma *value* (ou seja, uma propriedade com o nome &quot;value&quot;). Se o campo oculto em questão exigir que uma propriedade de valor padrão seja definida, essa propriedade deverá ser adicionada manualmente com uma das ferramentas CRX. O valor não pode ser adicionado com o próprio editor de diálogo. No entanto, quando a propriedade estiver presente, seu valor poderá ser editado com o editor da caixa de diálogo.

O segundo campo oculto pode ser visto clicando-o da seguinte maneira:

![hidden2](assets/hidden2.png)

As propriedades desse campo oculto são as seguintes:

![hidden_list_props2](assets/hidden_list_props2.png)

A propriedade de nome deste campo oculto é

`./jcr:content/par/text/sling:resourceType`

E o valor fixo especificado para essa propriedade é

`foundation/components/textimage`

Especifica que o componente a ser usado para renderizar o conteúdo de texto deste parágrafo é o *Imagem de texto* componente. Usar com o `isRichText` booleano especificado no outro campo oculto, o componente pode renderizar a cadeia de texto real armazenada em `./jcr:content/par/text/text` da forma desejada.

### Andaime com herança do MSM {#scaffolding-with-msm-inheritance}

Na interface clássica, o scaffolding é totalmente integrado à herança do MSM (quando aplicável).

Ao abrir uma página no **Andaime** modo (usando o ícone na parte inferior do sidekick) todos os componentes sujeitos a herança serão indicados por:

* um símbolo de bloqueio (para a maioria dos componentes; por exemplo, Texto e Título)
* uma máscara com o texto **Clique para cancelar a herança** (para componentes de Imagem)

Eles mostram que o componente não pode ser editado, até que a herança seja cancelada.

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>Isso é comparável ao [componentes herdados ao editar o conteúdo da página](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Clicar no símbolo de bloqueio ou no ícone de imagem permite interromper a herança:

* o símbolo muda para um cadeado aberto.
* depois de desbloqueado, é possível editar o conteúdo.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

Depois de desbloquear, você pode restaurar a herança clicando no símbolo de cadeado desbloqueado; isso perderá todas as edições que você fez.

>[!NOTE]
>
>Se a herança for cancelada no nível da página (na guia Live Copy das Propriedades da página), todos os componentes poderão ser editados no **Andaime** (são mostrados em um estado desbloqueado).
