---
title: Modelos no repositório
seo-title: Modelos no repositório
description: 'null'
seo-description: nulo
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 1%

---


# Modelos no repositório{#models-in-repository}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Um modelo contém um conjunto de tipos de dados que definem as propriedades que serão renderizadas pelos serviços de conteúdo. Um modelo também define as relações entre outros modelos para impor a integridade dos dados.

Como desenvolvedor, você deve se familiarizar com a estrutura Modelo no repositório. Você pode criar seus próprios modelos e entidades de acordo com suas necessidades de aplicativo.

## Criando Tipos de Modelo {#creating-model-types}

Há dois tipos de modelo fornecidos pelo sistema em */libs/settings/mobileapps/model-types*. Se desejar substituir os tipos de modelo do sistema, será necessário criar um nó *mobileapps/model-types* no nó de configuração no qual deseja que a substituição ocorra.

Por exemplo, se você criou configurações em */conf/myconf1* e */conf/myconf2* e deseja substituir os tipos de modelo do sistema somente em *conf1*, você criaria um nó *mobileapps/model-types* sob as configurações de *conf1*.

Se você deseja permitir que os tipos de dados sejam adicionados a um modelo, o tipo de modelo deve ter um nó filho chamado &#39;scaffolding&#39; do tipo &#39;cq:Page&#39; e um tipo de recurso de *wcm/scaffolding/components/scaffolding*.

A página de andaime também deve incluir uma propriedade *dataTypesConfig* no nó PageContent que indica que os modelos de tipos de dados criados a partir desse tipo poderão ser usados.

>[!NOTE]
>
>Uma **Andaime** é uma página que define os tipos de dados que podem ser editados por uma entidade com base no modelo. Cada tipo de dados também pode ser configurado para definir como o campo será apresentado na interface do usuário, bem como como como o valor de dados será persistente.

### Configuração de tipos de dados {#data-types-config}

O nó de configuração de tipos de dados contém uma lista de itens de tipo de dados. Cada item de tipo de dados especifica como um tipo de dados será exibido no editor de modelo, bem como como é necessário que seja persistente para uma eventual renderização por uma entidade.

| **Nome da Propriedade** | **Descrição** |
|---|---|
| fieldIcon | classe do ícone CoralUI para representar o tipo de dados |
| fieldPropResourceType | componente que renderizará todas as propriedades para configurar o tipo de dados |
| fieldProperties | lista de vários valores dos componentes de propriedade que são usados quando fieldPropResourceType é *mobileapps/caas/gui/components/editor/datatypes/field* |
| fieldResourceType | resourceType do nó persistente para o tipo de dados (ou seja, o componente que renderizará a propriedade no editor de entidades) |
| fieldViewResourceType | componente a ser usado para renderizar o tipo de dados na visualização do editor de modelo (fieldResourceType será usado se essa propriedade for omitida) |
| fieldTitle | nome do tipo de dados que será exibido no editor de modelo |
| multiFieldResourceType | tipo de recurso a ser usado no nó persistente quando vários valores forem selecionados |
| renderType | pista de renderização para renderização no cliente |

### Sobreposição de configuração de tipos de dados {#data-types-config-overlay}

A propriedade &#39;dataTypesConfig&#39; suporta a mesclagem de recursos Sling. Isso significa que os tipos de dados usados pelos tipos de modelo do sistema (ou até mesmo os tipos de modelo personalizados) podem ser personalizados usando nós de sobreposição.

Uma sobreposição de */libs/settings/mobileapps/models/formbuilderconfig/datatypes* precisará ser criada e personalizada conforme desejado.

Por exemplo, uma sobreposição para o tipo de dados String poderia ser adicionada para alterar fieldResourceType para um componente personalizado.

Para obter mais informações sobre a Mesclagem de recursos Sling, consulte [Usando a Fusão de recursos Sling em AEM](/help/sites-developing/sling-resource-merger.md).

![chlimage_1-7](assets/chlimage_1-7.png)

### Tipos de dados {#data-types}

Um tipo de dados de modelo é um componente de formulário capaz de incluir dados a serem incluídos ao publicar um formulário. O componente de tipo de dados pode ser tão complicado quanto desejado. Um exemplo de um tipo de dados personalizado pode ser um bloco de endereços para um país específico, para evitar ter que recriá-lo o tempo todo usando os tipos de dados primitivos.

Consulte &#39;/libs/mobileapps/caas/components/form/contentreference&#39; como um exemplo de um tipo de dados personalizado.

Todos os tipos de dados primitivos usam componentes de formulário Granite existentes. Consulte: [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

Qualquer tipo de dados personalizado pode ser adicionado a uma configuração de tipo de dados para uso pelo editor de modelo.

## Criando Modelos {#creating-models}

É possível criar modelos com start depois que todos os tipos de modelo e tipos de dados desejados forem desenvolvidos. Os autores acabarão usando modelos para criar entidades a partir das quais os serviços de conteúdo usam para renderizar seus dados.

A criação de um modelo consiste em escolher um tipo de modelo permitido com base na configuração atual e, em seguida, fornecer um título e uma descrição.

Para saber mais sobre como criar e gerenciar um modelo a partir do painel, consulte [Criação de um Modelo](/help/mobile/administer-mobile-apps.md) na seção de criação para aplicativos móveis.

### Propriedades de um Modelo {#properties-of-a-model}

A tabela a seguir mostra as propriedades definidas para um modelo:

| **Nome da Propriedade** | **Descrição** |
|---|---|
| Título do modelo | nome do modelo |
| Descrição | descrição do modelo |
| Miniatura  | imagem em miniatura do modelo |
| Tipo de modelo | tipo do modelo (pode ser uma sequência simples ou um caminho para um componente real) |
| Filhos permitidos | caminho de um modelo que tem permissão para ser filho deste modelo |
| Primários permitidos | caminho de um modelo que tem permissão para ser pai deste modelo |

>[!NOTE]
>
>As propriedades *filhos permitidos* e *pais permitidos* seguem as mesmas regras que os modelos de Página. Para obter mais informações, consulte [Modelos de página](/help/sites-developing/page-templates-static.md).
>
>Em referência à propriedade *Model Type*, todos os modelos devem ter um supertipo de *mobileapps/caas/components/data/entity*, mas podem ter um subtipo que permite que o delivery de conteúdo seja personalizado. Garantir que todos os tipos de modelo sejam exclusivos também pode ajudar clientes de serviços de conteúdo a distinguir entre objetos nos dados.

### Editando um Modelo {#editing-a-model}

A edição de um modelo envolve a abertura do formulário de diálogo de andaime associado a um modelo para edição. Geralmente, o andaime é um nó filho do modelo, mas pode ser localizado fora do modelo, se desejado, especificando seu caminho usando a propriedade &#39;cq:scaffolding&#39;. Isso é útil se você quiser compartilhar o mesmo andaime entre vários modelos que precisam ter propriedades diferentes.

Quando o andaime do modelo estiver localizado, o editor de modelo renderizará o que for encontrado em &#39;jcr:content/cq:dialog/content&#39;. Atualmente, apenas um layout fixo de até 3 colunas é suportado pelo mecanismo do cliente formbuilder. À direita da caixa de diálogo de formulário renderizado estará uma lista de todos os tipos de dados especificados na configuração de tipos de dados. Os tipos de dados podem ser editados clicando neles. O painel direito mudará para a guia de propriedades do tipo de dados selecionado. Novos tipos de dados podem ser adicionados arrastando-os para a tela de pré-visualização. Clicar em Salvar propaga as alterações no servidor. Clicar em Cancelar fecha o editor de modelo.

>[!NOTE]
>
>Todos os modelos são Modelos, portanto, eles seguem todas as regras de Modelos AEM. Isso permite o uso de propriedades como *allowParents* e *allowChildren* propriedades. Elas são eficazes ao criar novas Entidades com base em um modelo. As regras do modelo garantirão que as entidades só possam se basear em determinados modelos, dependendo de sua hierarquia.
>
>Para saber mais sobre como editar um modelo a partir do painel, consulte [Criar um modelo](/help/mobile/administer-mobile-apps.md) na seção de criação para aplicativos móveis.

### Modelos de sistema {#system-models}

Dois tipos de modelos de sistema predefinidos são fornecidos para reutilização de conteúdo simples. Esses modelos não podem ser editados.

**Modelo** de páginasO modelo de páginas fornece um método rápido para reutilizar o conteúdo existente de sites para delivery por serviços de conteúdo.

O resourceType das entidades com base no modelo Páginas é: mobileapps/caas/components/data/pages

Caminho: Caminho para uma página Sites. O conteúdo desse caminho (e seus filhos) será renderizado pelos manipuladores de serviço de conteúdo.

**Assets** ModelO modelo Ativos fornece um método rápido para reutilizar o conteúdo existente dos Ativos para delivery por serviços de conteúdo.

O resourceType das entidades com base no modelo Páginas é: *mobileapps/caas/components/data/assets.*

Lista do ativo: Lista de caminhos de Ativos. Cada ativo será adicionado como um nó de entidade filho com um resourceType de *wcm/Foundation/components/image*.

>[!NOTE]
>
>Para saber mais sobre como usar esses modelos para criar modelos a partir do painel, consulte [Criar um modelo](/help/mobile/administer-mobile-apps.md) na seção de criação para aplicativos móveis.
