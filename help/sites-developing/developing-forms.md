---
title: Desenvolvimento do Forms (interface clássica)
seo-title: Developing Forms (Classic UI)
description: Saiba como desenvolver formulários
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 5%

---

# Desenvolvimento do Forms (interface clássica){#developing-forms-classic-ui}

A estrutura básica de um formulário é:

* Início do formulário
* Elementos de formulário
* Fim do formulário

Todos estes são realizados com uma série de padrões [Componentes do formulário](/help/sites-authoring/default-components.md#form), disponível em uma instalação AEM padrão.

Além de [desenvolvimento de novos componentes](/help/sites-developing/developing-components-samples.md) para uso em formulários, você também pode:

* [Pré-carregar seu formulário com valores](#preloading-form-values)
* [Precarregar (determinados) campos com vários valores](#preloading-form-fields-with-multiple-values)
* [Desenvolver novas ações](#developing-your-own-form-actions)
* [Desenvolver novas restrições](#developing-your-own-form-constraints)
* [Mostrar ou ocultar campos de formulário específicos](#showing-and-hiding-form-components)

[Uso de scripts](#developing-scripts-for-use-with-forms) estender a funcionalidade, quando necessário.

>[!NOTE]
>
>Este documento se concentra no desenvolvimento de formulários usando o [Componentes básicos](/help/sites-authoring/default-components-foundation.md) na interface clássica. A Adobe recomenda o aproveitamento do novo [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e [Ocultar Condições](/help/sites-developing/hide-conditions.md) para desenvolvimento de formulário na interface habilitada para toque.

## Pré-carregar valores do formulário {#preloading-form-values}

O componente de início do formulário fornece um campo para a variável **Carregar caminho**, um caminho opcional que aponta para um nó no repositório.

O Caminho de carregamento é o caminho para as propriedades do nó, usado para carregar valores predefinidos em vários campos no formulário.

Isso é um campo opcional que especifica o caminho para um nó no repositório. Quando este nó tem propriedades que correspondem aos nomes do campo, os campos apropriados no formulário são pré-carregados com o valor dessas propriedades. Caso não exista nenhuma correspondência, o campo vai conter o valor padrão.

>[!NOTE]
>
>A [ação de formulário](#developing-your-own-form-actions) também pode definir o recurso do qual carregar os valores iniciais. Isso é feito usando `FormsHelper#setFormLoadResource` inside `init.jsp`.
>
>Somente se isso não for definido, o formulário será preenchido a partir do caminho definido no componente de formulário inicial pelo autor.

### Pré-carregamento de campos de formulário com vários valores {#preloading-form-fields-with-multiple-values}

Vários campos de formulário também têm a variável **Caminho de carregamento dos itens**, novamente um caminho opcional que aponta para um nó no repositório.

O **Caminho de carregamento dos itens** é o caminho para as propriedades do nó, usado para carregar valores predefinidos nesse campo específico do formulário, por exemplo, um [lista suspensa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [grupo de caixas de seleção](/help/sites-authoring/default-components-foundation.md#checkbox-group) ou [grupo de rádio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Exemplo - Pré-Carregamento De Uma Lista Suspensa Com Vários Valores {#example-preloading-a-dropdown-list-with-multiple-values}

Uma lista suspensa pode ser configurada com o intervalo de valores para a seleção.

O **Caminho de carregamento dos itens** pode ser usada para acessar uma lista de uma pasta no repositório e pré-carregá-las no campo :

1. Crie uma nova pasta sling ( `sling:Folder`) por exemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Adicionar uma nova propriedade (por exemplo, `myList`) do tipo string com vários valores ( `String[]`) para conter a lista de itens suspensos. O conteúdo também pode ser importado usando um script, como com um script JSP ou cURL em um script de shell.

1. Use o caminho completo na **Caminho de carregamento dos itens** campo : por exemplo, `/etc/designs/geometrixx/formlistvalues/myList`

Observe que se os valores na variável `String[]` são formatadas desta forma:

* `AL=Alabama`
* `AK=Alaska`
* etc.

então AEM gerará a lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esse recurso pode, por exemplo, ser aproveitado em uma configuração de vários idiomas.

### Desenvolvimento de suas próprias ações de formulário {#developing-your-own-form-actions}

Um formulário exige uma ação. Uma ação define a operação que é executada quando o formulário é enviado com os dados do usuário.

Uma variedade de ações são fornecidas com uma instalação padrão do AEM, essas ações podem ser vistas em:

`/libs/foundation/components/form/actions`

e na **Tipo de ação** lista de **Formulário** componente:

![chlimage_1-8](assets/chlimage_1-8.png)

Esta seção aborda como você pode desenvolver sua própria ação de formulário para inclusão nesta lista.

Você pode adicionar sua própria ação em `/apps` como se segue:

1. Criar um nó do tipo `sling:Folder`. Especifique um nome que reflita a ação a ser implementada.

   Por exemplo:

   `/apps/myProject/components/customFormAction`

1. Nesse nó, defina as seguintes propriedades e clique em **Salvar tudo** para continuar suas alterações:

   * `sling:resourceType` - definido como `foundation/components/form/action`

   * `componentGroup` - definir como `.hidden`

   * Opcionalmente:

      * `jcr:title` - especifique um título de sua escolha, que será exibido na lista suspensa de seleção. Se não estiver definido, o nome do nó será mostrado

      * `jcr:description` - insira uma descrição da sua escolha

1. Na pasta, crie um nó de diálogo:

   1. Adicione campos para que o autor possa editar a caixa de diálogo de formulários depois que a ação for escolhida.

1. Na pasta, crie:

   1. Um script de postagem.
O nome do script é `post.POST.<extension>`, por exemplo `post.POST.jsp`
O script de publicação é chamado quando um formulário é enviado para processar o formulário, ele contém o código que manipula os dados que chegam do formulário 
`POST`.

   1. Adicione um script forward que é chamado quando o formulário é enviado.
O nome do script é `forward.<extension`>, por exemplo `forward.jsp`
Esse script pode definir um caminho. A solicitação atual é encaminhada ao caminho especificado.
   A chamada necessária é `FormsHelper#setForwardPath` (2 variantes). Um caso típico é executar alguma validação, ou lógica, para encontrar o caminho de destino e, em seguida, avançar para esse caminho, permitindo que o servlet Sling POST padrão faça o armazenamento real no JCR.

   Também pode haver outro servlet que faça o processamento real, nesse caso, a ação do formulário e a variável `forward.jsp` atuaria somente como o código de &quot;cola&quot;. Um exemplo disso é a ação de email em `/libs/foundation/components/form/actions/mail`, que encaminha detalhes para `<currentpath>.mail.html`onde um servlet de email está.

   Assim:

   * a `post.POST.jsp` é útil para pequenas operações plenamente realizadas pela própria ação
   * enquanto a variável `forward.jsp` é útil quando somente a delegação é necessária.

   A ordem de execução dos scripts é:

   * Ao renderizar o formulário ( `GET`):

      1. `init.jsp`
      1. para todas as restrições do campo: `clientvalidation.jsp`
      1. validationRT do formulário: `clientvalidation.jsp`
      1. O formulário é carregado por meio do recurso de carregamento, se definido
      1. `addfields.jsp` ao processar `<form></form>`
   * ao manusear um formulário `POST`:

      1. `init.jsp`
      1. para todas as restrições do campo: `servervalidation.jsp`
      1. validationRT do formulário: `servervalidation.jsp`
      1. `forward.jsp`
      1. se um caminho de encaminhamento foi definido ( `FormsHelper.setForwardPath`), encaminhe a solicitação e chame `cleanup.jsp`

      1. se nenhum caminho de encaminhamento foi definido, chame `post.POST.jsp` (termina aqui, não `cleanup.jsp` chamado)




1. Novamente na pasta, opcionalmente, adicione:

   1. Um script para adicionar campos.
O nome do script é `addfields.<extension>`, por exemplo `addfields.jsp`
Um 
`addfields` O script é chamado imediatamente após o HTML para o início do formulário ser gravado. Isso permite que a ação adicione campos de entrada personalizados ou outro HTML dentro do formulário.

   1. Um script de inicialização.
O nome do script é `init.<extension>`, por exemplo `init.jsp`
Esse script é chamado quando o formulário é renderizado. Ele pode ser usado para inicializar ações específicas.

   1. Um script de limpeza.
O nome do script é `cleanup.<extension>`, por exemplo `cleanup.jsp`
Esse script pode ser usado para realizar a limpeza.

1. Use o **Forms** em um parsys. O **Tipo de ação** a lista suspensa agora incluirá sua nova ação.

   >[!NOTE]
   >
   >Para ver as ações padrão que fazem parte do produto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desenvolvimento de suas próprias restrições de formulário {#developing-your-own-form-constraints}

As restrições podem ser impostas em dois níveis:

* Para [campos individuais (consulte o procedimento a seguir)](#constraints-for-individual-fields)
* As [validação global de formulário](#form-global-constraints)

#### Restrições para campos individuais {#constraints-for-individual-fields}

É possível adicionar suas próprias restrições para um campo individual (em `/apps`) como segue:

1. Criar um nó do tipo `sling:Folder`. Especifique um nome que reflita a restrição a ser implementada.

   Por exemplo:

   `/apps/myProject/components/customFormConstraint`

1. Nesse nó, defina as seguintes propriedades e clique em **Salvar tudo** para continuar suas alterações:

   * `sling:resourceType` - defina como `foundation/components/form/constraint`

   * `constraintMessage` - uma mensagem personalizada que será exibida se o campo não for válido, de acordo com a restrição, quando o formulário for enviado

   * Opcionalmente:

      * `jcr:title` - especifique um título de sua escolha, que será exibido na lista de seleção. Se não estiver definido, o nome do nó será mostrado
      * `hint` - informações adicionais, para o usuário, sobre como usar o campo

1. Nessa pasta, você pode precisar dos seguintes scripts:

   * Um script de validação de cliente: O nome do script é `clientvalidation.<extension>`, por exemplo `clientvalidation.jsp`
Isso é chamado quando o campo de formulário é renderizado. Ele pode ser usado para criar o javascript cliente para validar o campo no cliente.

   * Um script de validação de servidor: O nome do script é `servervalidation.<extension>`, por exemplo `servervalidation.jsp`
Isso é chamado quando o formulário é enviado. Ele pode ser usado para validar o campo no servidor após o envio.

>[!NOTE]
>
>Restrições de amostra podem ser vistas em:
>
>`/libs/foundation/components/form/constraints`

#### Restrições globais de formulário {#form-global-constraints}

A validação global do formulário é especificada pela configuração de um tipo de recurso no componente do formulário inicial ( `validationRT`). Por exemplo:

`apps/myProject/components/form/validation`

Em seguida, é possível definir:

* a `clientvalidation.jsp` - inserido após os scripts de validação de cliente do campo
* e `servervalidation.jsp` - também é chamado após as validações individuais do servidor de campo em um `POST`.

### Mostrar e ocultar componentes de formulário {#showing-and-hiding-form-components}

É possível configurar o formulário para mostrar ou ocultar os componentes do formulário de acordo com o valor de outros campos no formulário.

Alterar a visibilidade de um campo do formulário é útil, quando o campo é necessário apenas em condições específicas. Por exemplo, em um formulário de feedback, uma pergunta pergunta faz com que os clientes queiram que as informações do produto sejam enviadas a eles por email. Ao selecionar sim, um campo de texto é exibido para permitir que o cliente digite seu endereço de email.

Use o **Editar Mostrar/Ocultar Regras** caixa de diálogo para especificar as condições em que um componente de formulário é exibido ou oculto.

![editor de texto](assets/showhideeditor.png)

Use os campos na parte superior da caixa de diálogo para especificar as seguintes informações:

* Se você estiver especificando as condições para ocultar ou mostrar o componente.
* Se alguma ou todas as condições precisam ser verdadeiras para mostrar ou ocultar o componente.

Uma ou mais condições são exibidas abaixo desses campos. Uma condição compara o valor de outro componente de formulário (no mesmo formulário) a um valor. Se o valor real no campo atender à condição, a condição avaliará como true. As condições incluem as seguintes informações:

* O Título do campo de formulário testado.
* Um operador.
* Um valor em relação a com o valor do campo é comparado.

Por exemplo, um componente Grupo de opções com o título `Receive email notifications?`* * contém `Yes` e `No` botões de opção. Um componente Campo de texto com o título de `Email Address` O usa a seguinte condição para que ela fique visível se `Yes` está selecionada:

![showwhidcondition](assets/showhidecondition.png)

No Javascript, as condições usam o valor da propriedade Nome do elemento para fazer referência aos campos. No exemplo anterior, a propriedade Nome do elemento do componente Grupo de opções é `contact`. O código a seguir é o código JavaScript equivalente para esse exemplo:

`((contact == "Yes"))`

**Para mostrar ou ocultar um componente de formulário:**

1. Edite o componente de formulário específico.

1. Selecionar **Mostrar / Ocultar** para abrir o **Editar Mostrar / Ocultar Regras** caixa de diálogo:

   * Na primeira lista suspensa, selecione **Mostrar** ou **Ocultar** para especificar se suas condições determinam se deseja mostrar ou ocultar o componente.

   * Na lista suspensa no final da linha superior, selecione:

      * **all** - se todas as condições devem ser verdadeiras para mostrar ou ocultar o componente
      * **any** - se apenas uma ou mais condições devem ser verdadeiras para mostrar ou ocultar o componente
   * Na linha de condição (uma é apresentada como padrão), selecione um componente, operador e especifique um valor.
   * Adicione mais condições, se necessário, clicando em **Adicionar condição**.

   Por exemplo:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Clique em **OK** para salvar a definição.

1. Depois de salvar sua definição, um **Editar regras** é exibido ao lado do **Mostrar / Ocultar** nas propriedades do componente de formulário. Clique neste link para abrir o **Editar Mostrar / Ocultar Regras** para fazer alterações.

   Clique em **OK** para salvar todas as alterações.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Os efeitos das definições Mostrar/Ocultar podem ser vistos e testados:
   >
   >* em **Visualizar** no ambiente do autor (precisa de um recarregamento de página ao alternar para a visualização)
   >
   >* no ambiente de publicação


#### Lidar com referências de componentes quebrados {#handling-broken-component-references}

As condições de mostrar/ocultar usam o valor da propriedade Nome do elemento para fazer referência a outros componentes no formulário. A configuração Mostrar/Ocultar é inválida quando qualquer uma das condições se refere a um componente que é excluído ou que teve a propriedade Nome do Elemento alterada. Quando essa situação ocorre, é necessário atualizar manualmente as condições ou ocorre um erro quando o formulário é carregado.

Quando a configuração Mostrar/Ocultar é inválida, a configuração é fornecida somente como código JavaScript. Edite o código para corrigir os problemas. O código usa a propriedade Nome do elemento que foi originalmente usada para fazer referência aos componentes.

### Desenvolvimento de scripts para uso com o Forms {#developing-scripts-for-use-with-forms}

Para obter mais informações sobre os elementos da API que podem ser usados ao gravar scripts, consulte o [javadocs relacionados a formulários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

É possível usar essa opção para ações como chamar um serviço antes do envio do formulário e cancelar o serviço em caso de falha:

* Definir o tipo de recurso de validação
* Incluir um script para validação:

   * No JSP, chame o serviço da Web e crie um `com.day.cq.wcm.foundation.forms.ValidationInfo` objeto que contém suas mensagens de erro. Se houver erros, os dados do formulário não serão publicados.
