---
title: Modelos de página - Estáticos
seo-title: Modelos de página - Estáticos
description: Um Modelo é usado para criar uma Página e define quais componentes podem ser usados dentro do escopo selecionado
seo-description: Um Modelo é usado para criar uma Página e define quais componentes podem ser usados dentro do escopo selecionado
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 3%

---


# Modelos de página - Estáticos{#page-templates-static}

Um Modelo é usado para criar uma Página e define quais componentes podem ser usados dentro do escopo selecionado. Um modelo é uma hierarquia de nós que tem a mesma estrutura que a página a ser criada, mas sem nenhum conteúdo real.

Cada modelo apresentará uma seleção de componentes disponíveis para uso.

* Os modelos são construídos de [Components](/help/sites-developing/components.md);
* Os componentes usam e permitem acesso a Widgets, e esses são usados para renderizar o Conteúdo.

>[!NOTE]
>
>[Os ](/help/sites-developing/page-templates-editable.md) modelos editáveis também estão disponíveis e são o tipo recomendado de modelos para maior flexibilidade e os recursos mais recentes.

## Propriedades e nós secundários de um modelo {#properties-and-child-nodes-of-a-template}

Um modelo é um nó do tipo cq:Template e tem as seguintes propriedades e nós secundários:

<table>
 <tbody>
  <tr>
   <td><strong>Nome <br /> </strong></td>
   <td><strong>Tipo <br /> </strong></td>
   <td><strong>Descrição <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>Modelo atual. Um modelo é do tipo de nó cq:Template.<br /> </td>
  </tr>
  <tr>
   <td> allowChildren </td>
   <td> Sequência de caracteres[]</td>
   <td>O caminho de um modelo que tem permissão para ser filho deste modelo.<br /> </td>
  </tr>
  <tr>
   <td> allowParents</td>
   <td> Sequência de caracteres[]</td>
   <td>O caminho de um modelo que tem permissão para ser pai deste modelo.<br /> </td>
  </tr>
  <tr>
   <td> allowPaths</td>
   <td> Sequência de caracteres[]</td>
   <td>O caminho de uma página que tem permissão para se basear neste modelo.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> Data</td>
   <td>Data de criação do modelo.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> Sequência de caracteres</td>
   <td>Descrição do modelo.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> Sequência de caracteres</td>
   <td>Título do modelo.<br /> </td>
  </tr>
  <tr>
   <td> classificação</td>
   <td> Longo</td>
   <td>Classificação do modelo. Usado para exibir o modelo na interface do usuário.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>Nó que contém o conteúdo do modelo.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>Miniatura do modelo.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>Ícone do modelo.<br /> </td>
  </tr>
 </tbody>
</table>

Um modelo é a base de uma página.

Para criar uma página, o modelo deve ser copiado (node-tree `/apps/<myapp>/template/<mytemplate>`) para a posição correspondente na árvore do site: isso é o que acontece se uma página for criada usando a guia **Sites**.

Essa ação de cópia também fornece à página seu conteúdo inicial (normalmente, somente conteúdo de nível superior) e a propriedade sling:resourceType, o caminho para o componente de página que é usado para renderizar a página (tudo no nó filho jcr:content).

## Como os Modelos são estruturados {#how-templates-are-structured}

Há dois aspectos a considerar:

* a estrutura do próprio modelo
* a estrutura do conteúdo produzido quando um modelo é usado

### A estrutura de um Modelo {#the-structure-of-a-template}

Um Modelo é criado em um nó do tipo **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

Podem ser definidas várias propriedades, em especial:

* **jcr:title** - title para o modelo; aparece na caixa de diálogo ao criar uma página.
* **jcr:description** - descrição do modelo; aparece na caixa de diálogo ao criar uma página.

Este nó contém um nó jcr:content (cq:PageContent) que pode ser usado como a base para o nó de conteúdo das páginas resultantes; isso faz referência, usando sling:resourceType, ao componente a ser usado para renderizar o conteúdo real de uma nova página.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Esse componente é usado para definir a estrutura e o design do conteúdo quando uma nova página é criada.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### O conteúdo produzido por um Modelo {#the-content-produced-by-a-template}

Os modelos são usados para criar páginas do tipo `cq:Page` (como mencionado anteriormente, uma página é um tipo especial de componente). Cada Página AEM tem um nó estruturado `jcr:content`. Isso:

* é do tipo cq:PageContent
* é um tipo de nó estruturado que contém uma definição de conteúdo definida
* tem uma propriedade `sling:resourceType` para fazer referência ao componente que contém os scripts sling usados para renderizar o conteúdo

### Modelos padrão {#default-templates}

AEM vem com vários modelos padrão disponíveis prontamente. Em alguns casos, talvez você queira usar os modelos como estão. Nesse caso, é necessário garantir que o modelo esteja disponível para seu site.

Por exemplo, AEM vem com vários modelos, incluindo uma página de conteúdo e um home page.

| **Título** | **Componente** | **Local** | **Propósito** |
|---|---|---|---|
| Página Inicial | homepage | geometrixx | O modelo de home page do Geometrixx. |
| Página de conteúdo | contentpage | geometrixx | O modelo da página de conteúdo do Geometrixx. |

#### Exibindo Modelos Padrão {#displaying-default-templates}

Para ver uma lista de todos os modelos no repositório, proceda da seguinte maneira:

1. No CRXDE Lite, abra o menu **Ferramentas** e clique em **Query**.

1. Na guia Query
1. Como **Type**, selecione **XPath**.

1. No campo de entrada **Query**, digite a seguinte string:
//element(*, cq:Template)

1. Clique em **Executar**. A lista é exibida na caixa de resultados.

Na maioria dos casos, você pegará um modelo existente e desenvolverá um novo para seu próprio uso. Consulte [Desenvolvimento de modelos de página](#developing-page-templates) para obter mais informações.

Para habilitar um modelo existente para seu site e desejar que ele seja exibido na caixa de diálogo **Criar página** ao criar uma página sob **Sites** a partir do console **Sites**, defina a propriedade allowPaths do nó modelo como: **/content(/.*)?**

## Como os modelos são aplicados {#how-template-designs-are-applied}

Quando os estilos são definidos na interface usando [Modo de design](/help/sites-authoring/default-components-designmode.md), o design é mantido no caminho exato do nó de conteúdo para o qual o estilo está sendo definido.

>[!CAUTION]
>
>O Adobe recomenda aplicar designs somente pelo [Modo Design](/help/sites-authoring/default-components-designmode.md).
>
>A modificação de designs no CRX DE por exemplo não uma prática recomendada e a aplicação desses designs pode variar do comportamento esperado.

Se os designs só forem aplicados usando o Modo de design, as seguintes seções, [Resolução do caminho de design](/help/sites-developing/page-templates-static.md#design-path-resolution), [Árvore de decisão](/help/sites-developing/page-templates-static.md#decision-tree) e [Exemplo](/help/sites-developing/page-templates-static.md#example) não serão aplicáveis.

### Resolução do caminho de design {#design-path-resolution}

Ao renderizar conteúdo com base em um modelo estático, AEM tentará aplicar o design e os estilos mais relevantes ao conteúdo com base em uma transversal da hierarquia de conteúdo.

AEM determina o estilo mais relevante para um nó de conteúdo na seguinte ordem:

* Se houver um design para o caminho completo e exato do nó de conteúdo (como quando o design é definido no Modo de design), use esse design.
* Se houver um design para o nó de conteúdo do pai, use esse design.
* Se houver um design para qualquer nó no caminho do nó de conteúdo, use esse design.

Nos dois últimos casos, se houver mais de um design aplicável, use o mais próximo do nó de conteúdo.

### Árvore de decisão {#decision-tree}

Esta é uma representação gráfica da lógica [Resolução do Caminho de Design](/help/sites-developing/page-templates-static.md#design-path-resolution).

![design_path_resolution](assets/design_path_resolution.png)

### Exemplo {#example}

Considere uma estrutura de conteúdo simples da seguinte maneira, na qual um design pode se aplicar a qualquer um dos nós:

`/root/branch/leaf`

A tabela a seguir descreve como AEM escolherá um design.

<table>
 <tbody>
  <tr>
   <td><strong>Encontrar Design Para<br /> </strong></td>
   <td><strong>Existem Designs Para<br /> </strong></td>
   <td><strong>Design escolhido<br /> </strong></td>
   <td><strong>Comentário</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>A correspondência mais exata é sempre feita.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>Volte para a correspondência mais próxima na árvore.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>Se tudo o resto falhar, veja o que resta.<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>Se não houver uma correspondência exata, pegue a que estiver na árvore.</p> <p>A suposição é que isso sempre será aplicável, mas mais para cima na árvore pode ser muito específico.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Desenvolvendo modelos de página {#developing-page-templates}

AEM modelos de página são simplesmente modelos usados para criar novas páginas. Eles podem conter o mínimo ou tanto conteúdo inicial quanto necessário, sendo sua função criar as estruturas de nó iniciais corretas, com as propriedades necessárias (principalmente sling:resourceType) definidas para permitir a edição e a renderização.

### Criando um novo modelo (com base em um modelo existente) {#creating-a-new-template-based-on-an-existing-template}

É necessário dizer que um novo modelo pode ser criado completamente do zero, mas geralmente um modelo existente será copiado e atualizado para economizar tempo e esforço. Por exemplo, os modelos dentro do Geometrixx podem ser usados para ajudá-lo a começar.

Para criar um novo modelo com base em um modelo existente:

1. Copie um modelo existente (de preferência, com uma definição o mais próxima possível do que você deseja obter) para um novo nó.

   Normalmente, os modelos são armazenados em **/apps/&lt;nome-do-site>/models/&lt;nome-do-modelo>**.

   >[!NOTE]
   >
   >A lista dos modelos disponíveis depende do local da nova página e das restrições de posicionamento especificadas em cada modelo. Consulte [Disponibilidade do modelo](#templateavailibility).

1. Altere **jcr:title** do novo nó de modelo para refletir sua nova função. Você também pode atualizar o **jcr:description**, se apropriado. Certifique-se de alterar a disponibilidade do modelo da página, conforme apropriado.

   >[!NOTE]
   >
   >Se quiser que seu modelo seja exibido na caixa de diálogo **Criar página** ao criar uma página sob **Sites** a partir do console **Sites**, defina a propriedade `allowedPaths` do nó de modelo como: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copie o componente no qual o modelo se baseia (isso é indicado pela propriedade **sling:resourceType** do nó **jcr:content** no modelo) para criar uma nova instância.

   Geralmente, os componentes são armazenados em **/apps/&lt;nome-do-site>/components/&lt;nome-do-componente>**.

1. Atualize **jcr:title** e **jcr:description** do novo componente.
1. Substitua thumbnail.png se quiser que uma nova imagem em miniatura seja mostrada na lista de seleção do modelo (tamanho 128 x 98 px).
1. Atualize o nó **sling:resourceType** do modelo **jcr:content** para fazer referência ao novo componente.
1. Faça outras alterações na funcionalidade ou design do modelo e/ou seu componente subjacente.

   >[!NOTE]
   >
   >As alterações feitas no nó **/apps/&lt;site>/models/&lt;nome-modelo>** afetarão a instância do modelo (como na lista de seleção).
   As alterações feitas no nó **/apps/&lt;site>/components/&lt;nome-do-componente>** afetarão a página de conteúdo criada quando o modelo for usado.

   Agora você pode criar uma página em seu site usando o novo modelo.

>[!NOTE]
A biblioteca do cliente do editor assume a presença da namespace `cq.shared` nas páginas de conteúdo e, se ela não estiver presente, o erro do JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará.
Todas as páginas de conteúdo de amostra contêm `cq.shared`, portanto, qualquer conteúdo baseado nelas inclui automaticamente `cq.shared`. No entanto, se você decidir criar suas próprias páginas de conteúdo do zero sem baseá-las no conteúdo de amostra, deverá incluir a namespace `cq.shared`.
Consulte [Usando bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Disponibilizando um Modelo Existente {#making-an-existing-template-available}

Este exemplo ilustra como permitir que um modelo seja usado para determinados caminhos de conteúdo. Os modelos que estão disponíveis para o autor da página ao criar novas páginas são determinados pela lógica definida em [Disponibilidade do modelo](/help/sites-developing/templates.md#template-availability).

1. No CRXDE Lite, navegue até o modelo que deseja usar para a sua página, por exemplo, o modelo de boletim.
1. Altere a propriedade `allowedPaths` e outras propriedades usadas para [disponibilidade do modelo](/help/sites-developing/templates.md#template-availability). Por exemplo, `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` significa que este modelo é permitido em qualquer caminho em `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
