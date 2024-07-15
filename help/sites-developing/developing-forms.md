---
title: Desenvolvimento do Forms (interface clássica)
description: Saiba como desenvolver formulários para a interface clássica do Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---

# Desenvolvimento do Forms (interface clássica){#developing-forms-classic-ui}

A estrutura básica de um formulário é:

* Início do formulário
* Elementos de formulário
* Fim do formulário

Tudo isso é realizado com uma série de [Componentes de formulário](/help/sites-authoring/default-components.md#form) padrão, disponíveis em uma instalação padrão do AEM.

Além de [desenvolver novos componentes](/help/sites-developing/developing-components-samples.md) para usar em seus formulários, você também pode:

* [Pré-carregar o formulário com valores](#preloading-form-values)
* [Pré-carregar (determinados) campos com vários valores](#preloading-form-fields-with-multiple-values)
* [Desenvolver novas ações](#developing-your-own-form-actions)
* [Desenvolver novas restrições](#developing-your-own-form-constraints)
* [Mostrar ou ocultar campos de formulário específicos](#showing-and-hiding-form-components)

[Usando scripts](#developing-scripts-for-use-with-forms) para estender a funcionalidade onde necessário.

>[!NOTE]
>
>Este documento se concentra no desenvolvimento de formulários usando os [Componentes de base](/help/sites-authoring/default-components-foundation.md) na interface clássica. A Adobe recomenda usar os novos [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e [Ocultar condições](/help/sites-developing/hide-conditions.md) para o desenvolvimento de formulários na interface habilitada para toque.

## Pré-carregando Valores de Formulário {#preloading-form-values}

O componente de início de formulário fornece um campo para o **Caminho de Carregamento**, um caminho opcional que aponta para um nó no repositório.

Carregar caminho é o caminho para as propriedades do nó usado para carregar valores predefinidos em vários campos no formulário.

Este é um campo opcional que especifica o caminho para um nó no repositório. Quando esse nó tem propriedades que correspondem aos nomes dos campos, os campos apropriados no formulário são pré-carregados com o valor dessas propriedades. Se não houver correspondência, o campo conterá o valor padrão.

>[!NOTE]
>
>Uma [ação de formulário](#developing-your-own-form-actions) também pode definir o recurso do qual carregar os valores iniciais. Isso é feito usando `FormsHelper#setFormLoadResource` dentro de `init.jsp`.
>
>Somente se isso não for definido, o formulário será preenchido a partir do caminho definido no componente Formulário inicial pelo autor.

### Pré-carregamento de campos de formulário com vários valores {#preloading-form-fields-with-multiple-values}

Vários campos de formulário também têm o **Caminho de Carregamento de Itens**, novamente um caminho opcional que aponta para um nó no repositório.

O **Caminho de Carregamento de Itens** é o caminho para as propriedades do nó usado para carregar valores predefinidos nesse campo específico no formulário, por exemplo, uma [lista suspensa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [grupo de caixas de seleção](/help/sites-authoring/default-components-foundation.md#checkbox-group) ou [grupo de opções](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Exemplo - Pré-carregamento De Uma Lista Suspensa Com Vários Valores {#example-preloading-a-dropdown-list-with-multiple-values}

Uma lista suspensa pode ser configurada com o intervalo de valores para seleção.

O **Caminho de Carregamento de Itens** pode ser usado para acessar uma lista de uma pasta no repositório e pré-carregá-los no campo:

1. Criar uma pasta do sling ( `sling:Folder`)
por exemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Adicione uma nova propriedade (por exemplo, `myList`) do tipo cadeia de caracteres de vários valores ( `String[]`) para conter a lista de itens suspensos. O conteúdo também pode ser importado usando um script, como com um script JSP ou cURL em um script de shell.

1. Use o caminho completo no campo **Caminho de Carregamento de Itens**:
por exemplo, `/etc/designs/geometrixx/formlistvalues/myList`

Observe que se os valores em `String[]` forem do formato formatado desta forma:

* `AL=Alabama`
* `AK=Alaska`

e assim por diante, o AEM gera a lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esse recurso pode, por exemplo, ser bem usado em uma configuração multilíngue.

### Desenvolver suas próprias ações de formulário {#developing-your-own-form-actions}

Um formulário precisa de uma ação. Uma ação define a operação que é executada quando o formulário é enviado com os dados do usuário.

Uma série de ações é fornecida com uma instalação padrão de AEM, que podem ser vistas em:

`/libs/foundation/components/form/actions`

e na lista **Tipo de Ação** do componente **Formulário**:

![chlimage_1-8](assets/chlimage_1-8.png)

Esta seção aborda como você pode desenvolver sua própria ação de formulário para inclusão nesta lista.

Você pode adicionar sua própria ação em `/apps` da seguinte maneira:

1. Crie um nó do tipo `sling:Folder`. Especifique um nome que reflita a ação a ser implementada.

   Por exemplo:

   `/apps/myProject/components/customFormAction`

1. Neste nó, defina as seguintes propriedades e clique em **Salvar tudo** para manter suas alterações:

   * `sling:resourceType` - definido como `foundation/components/form/action`

   * `componentGroup` - definir como `.hidden`

   * Opcionalmente:

      * `jcr:title` - especifique um título de sua escolha, ele aparecerá na lista suspensa de seleção. Se não estiver definido, o nome do nó será mostrado

      * `jcr:description` - insira uma descrição de sua escolha

1. Na pasta, crie um nó de diálogo:

   1. Adicione campos para que o autor possa editar a caixa de diálogo de formulários depois que a ação for escolhida.

1. Na pasta, crie:

   1. Um script post.
O nome do script é `post.POST.<extension>`, por exemplo, `post.POST.jsp`
O script post é chamado quando um formulário é enviado para processar o formulário, ele contém o código que manipula os dados que chegam do formulário `POST`.

   1. Adicione um script de encaminhamento que é chamado quando o formulário é enviado.
O nome do script é `forward.<extension`>, por exemplo, `forward.jsp`
Este script pode definir um caminho. A solicitação atual é então encaminhada para o caminho especificado.

   A chamada necessária é `FormsHelper#setForwardPath` (2 variantes). Um caso típico é executar alguma validação, ou lógica, para encontrar o caminho de destino e, em seguida, encaminhar para esse caminho, permitindo que o servlet Sling POST padrão faça o armazenamento real no JCR.

   Também pode haver outro servlet que faça o processamento real; nesse caso, a ação do formulário e `forward.jsp` atuariam somente como o código &quot;cola&quot;. Um exemplo disso é a ação de email em `/libs/foundation/components/form/actions/mail`, que encaminha detalhes para `<currentpath>.mail.html`onde está um servlet de email.

   Assim:

   * um `post.POST.jsp` é útil para pequenas operações que são totalmente realizadas pela própria ação
   * enquanto o `forward.jsp` é útil quando apenas a delegação é necessária.

   A ordem de execução dos scripts é:

   * Ao renderizar o formulário ( `GET`):

      1. `init.jsp`
      1. para todas as restrições do campo: `clientvalidation.jsp`
      1. validationRT do formulário: `clientvalidation.jsp`
      1. o formulário é carregado por meio do recurso de carga, se definido
      1. `addfields.jsp` enquanto estava dentro da renderização `<form></form>`

   * ao manipular um formulário `POST`:

      1. `init.jsp`
      1. para todas as restrições do campo: `servervalidation.jsp`
      1. validationRT do formulário: `servervalidation.jsp`
      1. `forward.jsp`
      1. se um caminho de encaminhamento foi definido ( `FormsHelper.setForwardPath`), encaminhe a solicitação e, em seguida, chame `cleanup.jsp`

      1. se nenhum caminho de encaminhamento foi definido, chame `post.POST.jsp` (termina aqui, nenhum `cleanup.jsp` foi chamado)

1. Novamente, na pasta, adicione opcionalmente:

   1. Um script para adicionar campos.
O nome do script é `addfields.<extension>`, por exemplo, `addfields.jsp`
Um script `addfields` é chamado imediatamente após o HTML do início do formulário ser gravado. Isso permite que a ação adicione campos de entrada personalizados ou outro HTML semelhante dentro do formulário.

   1. Um script de inicialização.
O nome do script é `init.<extension>`, por exemplo, `init.jsp`
Esse script é chamado quando o formulário é renderizado. Ele pode ser usado para inicializar especificações de ação.

   1. Um script de limpeza.
O nome do script é `cleanup.<extension>`, por exemplo, `cleanup.jsp`
Esse script pode ser usado para executar a limpeza.

1. Use o componente **Forms** em um parsys. O menu suspenso **Tipo de ação** agora incluirá sua nova ação.

   >[!NOTE]
   >
   >Para ver as ações padrão que fazem parte do produto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desenvolver suas próprias restrições de formulário {#developing-your-own-form-constraints}

Restrições podem ser impostas em dois níveis:

* Para [campos individuais (consulte o seguinte procedimento)](#constraints-for-individual-fields)
* Como [validação de formulário global](#form-global-constraints)

#### Restrições para Campos Individuais {#constraints-for-individual-fields}

Você pode adicionar suas próprias restrições para um campo individual (em `/apps`) da seguinte maneira:

1. Crie um nó do tipo `sling:Folder`. Especifique um nome que reflita a restrição a ser implementada.

   Por exemplo:

   `/apps/myProject/components/customFormConstraint`

1. Neste nó, defina as seguintes propriedades e clique em **Salvar tudo** para manter suas alterações:

   * `sling:resourceType` - definido como `foundation/components/form/constraint`

   * `constraintMessage` - uma mensagem personalizada que é mostrada se o campo não é válido, de acordo com a restrição, quando o formulário é enviado

   * Opcionalmente:

      * `jcr:title` - especifique um título de sua escolha, ele aparecerá na lista de seleção. Se não estiver definido, o nome do nó será mostrado
      * `hint` - informações adicionais, para o usuário, sobre como usar o campo

1. Nessa pasta, você pode precisar dos seguintes scripts:

   * Um script de validação de cliente:
O nome do script é `clientvalidation.<extension>`, por exemplo, `clientvalidation.jsp`
Isso é chamado quando o campo de formulário é renderizado. Ele pode ser usado para criar o javascript do cliente para validar o campo no cliente.

   * Um script de validação do servidor:
O nome do script é `servervalidation.<extension>`, por exemplo, `servervalidation.jsp`
Isso é chamado quando o formulário é enviado. Ele pode ser usado para validar o campo no servidor após ser enviado.

>[!NOTE]
>
>Restrições de exemplo podem ser vistas em:
>
>`/libs/foundation/components/form/constraints`

#### Restrições globais de forma {#form-global-constraints}

A validação global de formulário é especificada pela configuração de um tipo de recurso no componente de formulário inicial ( `validationRT`). Por exemplo:

`apps/myProject/components/form/validation`

Em seguida, você pode definir:

* um `clientvalidation.jsp` - inserido após os scripts de validação de cliente do campo
* e um `servervalidation.jsp` - também chamado após as validações individuais do servidor de campo em um `POST`.

### Mostrando e ocultando componentes de formulário {#showing-and-hiding-form-components}

Você pode configurar o formulário para mostrar ou ocultar componentes do formulário de acordo com o valor de outros campos no formulário.

Alterar a visibilidade de um campo de formulário é útil quando o campo é necessário somente em condições específicas. Por exemplo, em um formulário de feedback, uma pergunta pergunta pergunta aos clientes se eles desejam que as informações do produto sejam enviadas a eles por email. Ao selecionar sim, um campo de texto aparece para permitir que o cliente digite seu endereço de email.

Use a caixa de diálogo **Editar regras de exibição/ocultação** para especificar as condições em que um componente de formulário é exibido ou ocultado.

![showhideeditor](assets/showhideeditor.png)

Use os campos na parte superior da caixa de diálogo para especificar as seguintes informações:

* Se você está especificando condições para ocultar ou mostrar o componente.
* Se alguma ou todas as condições precisam ser verdadeiras para mostrar ou ocultar o componente.

Uma ou mais condições aparecem abaixo desses campos. Uma condição compara o valor de outro componente de formulário (no mesmo formulário) a um valor. Se o valor real no campo atender à condição, a condição será avaliada como verdadeira. As condições incluem as seguintes informações:

* O Título do campo de formulário que é testado.
* Um operador.
* Um valor em relação ao com o valor do campo é comparado.

Por exemplo, um componente Grupo de opções com o título `Receive email notifications?`* * contém `Yes` e `No` botões de opção. Um componente Campo de Texto com o título `Email Address` usa a seguinte condição para que fique visível se `Yes` for selecionado:

![showhidecondition](assets/showhidecondition.png)

No JavaScript, as condições usam o valor da propriedade Nome do elemento para se referir aos campos. No exemplo anterior, a propriedade Nome do Elemento do componente Grupo de opções é `contact`. O código a seguir é o código JavaScript equivalente para esse exemplo:

`((contact == "Yes"))`

**Para mostrar ou ocultar um componente de formulário:**

1. Edite o componente de formulário específico.

1. Selecione **Mostrar / Ocultar** para abrir a caixa de diálogo **Editar Mostrar / Ocultar Regras**:

   * Na primeira lista suspensa, selecione **Mostrar** ou **Ocultar** para especificar se suas condições determinam se o componente deve ser mostrado ou ocultado.

   * Na lista suspensa no final da linha superior, selecione:

      * **todos** - se todas as condições forem verdadeiras para mostrar ou ocultar o componente
      * **any** - se apenas uma ou mais condições precisarem ser verdadeiras para mostrar ou ocultar o componente

   * Na linha de condição (uma é apresentada como padrão), selecione um componente, operador e especifique um valor.
   * Adicione mais condições, se necessário, clicando em **Adicionar Condição**.

   Por exemplo:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Clique em **OK** para salvar a definição.

1. Depois que você salvar a definição, um link **Editar regras** aparecerá ao lado da opção **Mostrar/Ocultar** nas propriedades do componente de formulário. Clique neste link para abrir a caixa de diálogo **Editar Mostrar/Ocultar Regras** para fazer alterações.

   Clique em **OK** para salvar todas as alterações.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Os efeitos das definições Mostrar/Ocultar podem ser vistos e testados:
   >
   >* no modo **Visualização** no ambiente do autor (precisa de um recarregamento de página ao alternar para visualização pela primeira vez)
   >
   >* no ambiente de publicação

#### Manipular referências de componentes corrompidos {#handling-broken-component-references}

As condições de mostrar/ocultar usam o valor da propriedade Nome do elemento para fazer referência a outros componentes no formulário. A configuração Mostrar/Ocultar é inválida quando qualquer uma das condições se refere a um componente excluído ou teve a propriedade Nome do elemento alterada. Quando essa situação ocorrer, você precisará atualizar manualmente as condições ou ocorrerá um erro quando o formulário for carregado.

Quando a configuração Mostrar/Ocultar é inválida, a configuração é fornecida somente como código JavaScript. Edite o código para corrigir os problemas. O código usa a propriedade Nome do Elemento que foi originalmente usada para fazer referência aos componentes.

### Desenvolvimento de scripts para uso com o Forms {#developing-scripts-for-use-with-forms}

Para obter mais informações sobre os elementos da API que podem ser usados ao gravar scripts, consulte os [javadocs relacionados a formulários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Você pode usar isso para ações como chamar um serviço antes que o formulário seja enviado e cancelar o serviço se ele falhar:

* Definir o tipo de recurso de validação
* Incluir um script para validação:

   * No JSP, chame o serviço da Web e crie um objeto `com.day.cq.wcm.foundation.forms.ValidationInfo` contendo suas mensagens de erro. Se houver erros, os dados do formulário não serão publicados.
