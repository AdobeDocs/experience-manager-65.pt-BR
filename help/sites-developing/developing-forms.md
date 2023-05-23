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
ht-degree: 0%

---

# Desenvolvimento do Forms (interface clássica){#developing-forms-classic-ui}

A estrutura básica de um formulário é:

* Início do formulário
* Elementos de formulário
* Fim do formulário

Todos esses são realizados com uma série de [Componentes de formulário](/help/sites-authoring/default-components.md#form), disponível em uma instalação padrão do AEM.

Além de [desenvolvimento de novos componentes](/help/sites-developing/developing-components-samples.md) para usar nos formulários, você também pode:

* [Pré-carregar o formulário com valores](#preloading-form-values)
* [Pré-carregar (determinados) campos com vários valores](#preloading-form-fields-with-multiple-values)
* [Desenvolver novas ações](#developing-your-own-form-actions)
* [Desenvolver novas restrições](#developing-your-own-form-constraints)
* [Mostrar ou ocultar campos de formulário específicos](#showing-and-hiding-form-components)

[Uso de scripts](#developing-scripts-for-use-with-forms) para estender a funcionalidade onde necessário.

>[!NOTE]
>
>Este documento se concentra no desenvolvimento de formulários usando o [Componentes de base](/help/sites-authoring/default-components-foundation.md) na interface clássica. A Adobe recomenda aproveitar o novo [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e [Ocultar condições](/help/sites-developing/hide-conditions.md) para desenvolvimento de formulários na interface habilitada para toque.

## Pré-carregando Valores de Formulário {#preloading-form-values}

O componente de início do formulário fornece um campo para a **Carregar caminho**, um caminho opcional que aponta para um nó no repositório.

Carregar caminho é o caminho para as propriedades do nó usado para carregar valores predefinidos em vários campos no formulário.

Este é um campo opcional que especifica o caminho para um nó no repositório. Quando esse nó tem propriedades que correspondem aos nomes dos campos, os campos apropriados no formulário são pré-carregados com o valor dessas propriedades. Se não houver correspondência, o campo conterá o valor padrão.

>[!NOTE]
>
>A [ação de formulário](#developing-your-own-form-actions) O também pode definir o recurso do qual carregar os valores iniciais. Isso é feito usando `FormsHelper#setFormLoadResource` dentro `init.jsp`.
>
>Somente se isso não for definido, o formulário será preenchido a partir do caminho definido no componente Formulário inicial pelo autor.

### Pré-carregamento de campos de formulário com vários valores {#preloading-form-fields-with-multiple-values}

Vários campos de formulário também têm a função **Caminho de carregamento de itens**, novamente um caminho opcional que aponta para um nó no repositório.

A variável **Caminho de carregamento de itens** é o caminho para as propriedades do nó usado para carregar valores predefinidos nesse campo específico do formulário, por exemplo, um [lista suspensa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [grupo de caixas de seleção](/help/sites-authoring/default-components-foundation.md#checkbox-group) ou [grupo de rádio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Exemplo - Pré-carregamento De Uma Lista Suspensa Com Vários Valores {#example-preloading-a-dropdown-list-with-multiple-values}

Uma lista suspensa pode ser configurada com o intervalo de valores para seleção.

A variável **Caminho de carregamento de itens** O pode ser usado para acessar uma lista de uma pasta no repositório e pré-carregá-la no campo:

1. Criar uma nova pasta do sling ( `sling:Folder`) por exemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Adicione uma nova propriedade (por exemplo, `myList`) do tipo sequência de caracteres de vários valores ( `String[]`) para conter a lista de itens suspensos. O conteúdo também pode ser importado usando um script, como com um script JSP ou cURL em um script de shell.

1. Use o caminho completo na variável **Caminho de carregamento de itens** field: por exemplo, `/etc/designs/geometrixx/formlistvalues/myList`

Observe que se os valores no campo `String[]` são do formato assim:

* `AL=Alabama`
* `AK=Alaska`
* etc.

em seguida, o AEM gerará a lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esse recurso pode, por exemplo, ser bem usado em uma configuração multilíngue.

### Desenvolver suas próprias ações de formulário {#developing-your-own-form-actions}

Um formulário precisa de uma ação. Uma ação define a operação que é executada quando o formulário é enviado com os dados do usuário.

Uma série de ações é fornecida com uma instalação padrão de AEM, que podem ser vistas em:

`/libs/foundation/components/form/actions`

e no **Tipo de ação** lista de **Formulário** componente:

![chlimage_1-8](assets/chlimage_1-8.png)

Esta seção aborda como você pode desenvolver sua própria ação de formulário para inclusão nesta lista.

Você pode adicionar sua própria ação em `/apps` do seguinte modo:

1. Criar um nó do tipo `sling:Folder`. Especifique um nome que reflita a ação a ser implementada.

   Por exemplo:

   `/apps/myProject/components/customFormAction`

1. Nesse nó, defina as seguintes propriedades e clique em **Salvar tudo** para manter suas alterações:

   * `sling:resourceType` - definir como `foundation/components/form/action`

   * `componentGroup` - definir como `.hidden`

   * Opcionalmente:

      * `jcr:title` - especifique um título de sua escolha, ele será exibido na lista suspensa de seleção. Se não estiver definido, o nome do nó será mostrado

      * `jcr:description` - insira uma descrição de sua escolha

1. Na pasta, crie um nó de diálogo:

   1. Adicione campos para que o autor possa editar a caixa de diálogo de formulários depois que a ação for escolhida.

1. Na pasta, crie:

   1. Um script post.
O nome do script é `post.POST.<extension>`, por exemplo, `post.POST.jsp`
O script post é chamado quando um formulário é enviado para processar o formulário, ele contém o código que lida com os dados que chegam do formulário 
`POST`.

   1. Adicione um script de encaminhamento que é chamado quando o formulário é enviado.
O nome do script é `forward.<extension`>, por exemplo `forward.jsp`
Este script pode definir um caminho. A solicitação atual é então encaminhada para o caminho especificado.
   A chamada necessária é `FormsHelper#setForwardPath` (2 variantes) Um caso típico é executar alguma validação, ou lógica, para encontrar o caminho de destino e, em seguida, encaminhar para esse caminho, permitindo que o servlet Sling POST padrão faça o armazenamento real no JCR.

   Também pode haver outro servlet que faça o processamento real, nesse caso, a ação do formulário e o `forward.jsp` agiria somente como o código de &quot;cola&quot;. Um exemplo disso é a ação de email em `/libs/foundation/components/form/actions/mail`, que encaminha detalhes para `<currentpath>.mail.html`onde está um servlet de e-mail.

   Assim:

   * a `post.POST.jsp` é útil para pequenas operações totalmente realizadas pela própria ação
   * enquanto a variável `forward.jsp` é útil quando somente a delegação é necessária.

   A ordem de execução dos scripts é:

   * Ao renderizar o formulário ( `GET`):

      1. `init.jsp`
      1. para todas as restrições do campo: `clientvalidation.jsp`
      1. validationRT do formulário: `clientvalidation.jsp`
      1. o formulário é carregado por meio do recurso de carga, se definido
      1. `addfields.jsp` durante a renderização `<form></form>`
   * ao manusear um formulário `POST`:

      1. `init.jsp`
      1. para todas as restrições do campo: `servervalidation.jsp`
      1. validationRT do formulário: `servervalidation.jsp`
      1. `forward.jsp`
      1. se um caminho de encaminhamento foi definido ( `FormsHelper.setForwardPath`), encaminhe a solicitação e, em seguida, chame `cleanup.jsp`

      1. se nenhum caminho de encaminhamento foi definido, chame `post.POST.jsp` (termina aqui, não `cleanup.jsp` chamado)




1. Novamente, na pasta, adicione opcionalmente:

   1. Um script para adicionar campos.
O nome do script é `addfields.<extension>`, por exemplo, `addfields.jsp`
Um 
`addfields` O script é chamado imediatamente após o HTML para o início do formulário ser gravado. Isso permite que a ação adicione campos de entrada personalizados ou outro HTML semelhante dentro do formulário.

   1. Um script de inicialização.
O nome do script é `init.<extension>`, por exemplo, `init.jsp`
Esse script é chamado quando o formulário é renderizado. Ele pode ser usado para inicializar especificações de ação.

   1. Um script de limpeza.
O nome do script é `cleanup.<extension>`, por exemplo, `cleanup.jsp`
Esse script pode ser usado para executar a limpeza.

1. Use o **Forms** em um parsys. A variável **Tipo de ação** agora incluirá sua nova ação.

   >[!NOTE]
   >
   >Para ver as ações padrão que fazem parte do produto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desenvolver suas próprias restrições de formulário {#developing-your-own-form-constraints}

Restrições podem ser impostas em dois níveis:

* Para [campos individuais (consulte o procedimento a seguir)](#constraints-for-individual-fields)
* Como [validação do formulário global](#form-global-constraints)

#### Restrições para Campos Individuais {#constraints-for-individual-fields}

Você pode adicionar suas próprias restrições para um campo individual (em `/apps`) do seguinte modo:

1. Criar um nó do tipo `sling:Folder`. Especifique um nome que reflita a restrição a ser implementada.

   Por exemplo:

   `/apps/myProject/components/customFormConstraint`

1. Nesse nó, defina as seguintes propriedades e clique em **Salvar tudo** para manter suas alterações:

   * `sling:resourceType` - defina como `foundation/components/form/constraint`

   * `constraintMessage` - uma mensagem personalizada que será exibida se o campo não for válido, de acordo com a restrição, quando o formulário for enviado

   * Opcionalmente:

      * `jcr:title` - especifique um título de sua escolha, ele será exibido na lista de seleção. Se não estiver definido, o nome do nó será mostrado
      * `hint` - informações adicionais, para o usuário, sobre como usar o campo

1. Nessa pasta, você pode precisar dos seguintes scripts:

   * Um script de validação de cliente: O nome do script é `clientvalidation.<extension>`, por exemplo, `clientvalidation.jsp`
Isso é chamado quando o campo de formulário é renderizado. Ele pode ser usado para criar o javascript do cliente para validar o campo no cliente.

   * Um script de validação de servidor: o nome do script é `servervalidation.<extension>`, por exemplo, `servervalidation.jsp`
Isso é chamado quando o formulário é enviado. Ele pode ser usado para validar o campo no servidor após ser enviado.

>[!NOTE]
>
>Restrições de exemplo podem ser vistas em:
>
>`/libs/foundation/components/form/constraints`

#### Restrições globais de forma {#form-global-constraints}

A validação global de formulário é especificada configurando um tipo de recurso no componente de formulário inicial ( `validationRT`). Por exemplo:

`apps/myProject/components/form/validation`

Em seguida, você pode definir:

* a `clientvalidation.jsp` - inserido após os scripts de validação do cliente do campo
* e uma `servervalidation.jsp` - também chamado após as validações individuais do servidor de campo em um `POST`.

### Mostrando e ocultando componentes de formulário {#showing-and-hiding-form-components}

Você pode configurar o formulário para mostrar ou ocultar componentes do formulário de acordo com o valor de outros campos no formulário.

Alterar a visibilidade de um campo de formulário é útil quando o campo é necessário somente em condições específicas. Por exemplo, em um formulário de feedback, uma pergunta pergunta pergunta aos clientes se eles desejam que as informações do produto sejam enviadas a eles por email. Ao selecionar sim, um campo de texto aparece para permitir que o cliente digite seu endereço de email.

Use o **Editar regras de Mostrar/Ocultar** caixa de diálogo para especificar as condições sob as quais um componente de formulário é exibido ou ocultado.

![show whideeditor](assets/showhideeditor.png)

Use os campos na parte superior da caixa de diálogo para especificar as seguintes informações:

* Se você está especificando condições para ocultar ou mostrar o componente.
* Se alguma ou todas as condições precisam ser verdadeiras para mostrar ou ocultar o componente.

Uma ou mais condições aparecem abaixo desses campos. Uma condição compara o valor de outro componente de formulário (no mesmo formulário) a um valor. Se o valor real no campo atender à condição, a condição será avaliada como verdadeira. As condições incluem as seguintes informações:

* O Título do campo de formulário que é testado.
* Um operador.
* Um valor em relação ao com o valor do campo é comparado.

Por exemplo, um componente Grupo de opções com o título `Receive email notifications?`* * contém `Yes` e `No` botões de opção. Um componente Campo de texto com o título de `Email Address` O usa a seguinte condição para que seja visível se `Yes` está selecionado:

![show whidecondition](assets/showhidecondition.png)

No JavaScript, as condições usam o valor da propriedade Nome do elemento para se referir aos campos. No exemplo anterior, a propriedade Nome do elemento do componente Grupo de opções é `contact`. O código a seguir é o código JavaScript equivalente para esse exemplo:

`((contact == "Yes"))`

**Para mostrar ou ocultar um componente de formulário:**

1. Edite o componente de formulário específico.

1. Selecionar **Mostrar/Ocultar** para abrir o **Editar regras de Mostrar/Ocultar** diálogo:

   * Na primeira lista suspensa, selecione **Mostrar** ou **Ocultar** para especificar se as condições determinam se o componente deve ser mostrado ou ocultado.

   * Na lista suspensa no final da linha superior, selecione:

      * **all** - se todas as condições forem verdadeiras para mostrar ou ocultar o componente
      * **qualquer** - se apenas uma ou mais condições forem verdadeiras para mostrar ou ocultar o componente
   * Na linha de condição (uma é apresentada como padrão), selecione um componente, operador e especifique um valor.
   * Adicione mais condições, se necessário, clicando em **Adicionar Condição**.

   Por exemplo:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Clique em **OK** para salvar a definição.

1. Depois de salvar sua definição, uma **Editar regras** é exibido ao lado da tag **Mostrar/Ocultar** nas propriedades do componente de formulário. Clique neste link para abrir a **Editar regras de Mostrar/Ocultar** para fazer alterações.

   Clique em **OK** para salvar todas as alterações.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Os efeitos das definições Mostrar/Ocultar podem ser vistos e testados:
   >
   >* in **Visualizar** no ambiente do autor (precisa de um recarregamento de página ao alternar para visualização pela primeira vez)
   >
   >* no ambiente de publicação


#### Manipular referências de componentes corrompidos {#handling-broken-component-references}

As condições de mostrar/ocultar usam o valor da propriedade Nome do elemento para fazer referência a outros componentes no formulário. A configuração Mostrar/Ocultar é inválida quando qualquer uma das condições se refere a um componente excluído ou teve a propriedade Nome do elemento alterada. Quando essa situação ocorrer, você precisará atualizar manualmente as condições ou ocorrerá um erro quando o formulário for carregado.

Quando a configuração Mostrar/Ocultar é inválida, a configuração é fornecida somente como código JavaScript. Edite o código para corrigir os problemas. O código usa a propriedade Nome do Elemento que foi originalmente usada para fazer referência aos componentes.

### Desenvolvimento de scripts para uso com o Forms {#developing-scripts-for-use-with-forms}

Para obter mais informações sobre os elementos da API que podem ser usados ao gravar scripts, consulte a [javadocs relacionados a formulários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Você pode usar isso para ações como chamar um serviço antes que o formulário seja enviado e cancelar o serviço se ele falhar:

* Definir o tipo de recurso de validação
* Incluir um script para validação:

   * No JSP, chame o serviço da Web e crie um `com.day.cq.wcm.foundation.forms.ValidationInfo` objeto contendo suas mensagens de erro. Se houver erros, os dados do formulário não serão publicados.
