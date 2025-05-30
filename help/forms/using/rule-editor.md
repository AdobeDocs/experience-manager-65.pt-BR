---
title: Editor de regras de formulários adaptáveis
description: O editor de regras de formulários adaptáveis permite adicionar comportamento dinâmico e criar lógica complexa em formulários sem codificação ou script.
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Adaptive Forms,Foundation Components
discoiquuid: 1b905e66-dc05-4f14-8025-62a78feef12a
docset: aem65
exl-id: c611a1f8-9d94-47f3-bed3-59eef722bf98
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '6607'
ht-degree: 0%

---

# Editor de regras de formulários adaptáveis{#adaptive-forms-rule-editor}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

## Visão geral {#overview}

O recurso do editor de regras no Adobe Experience Manager Forms permite que usuários e desenvolvedores de negócios de formulários gravem regras em objetos de formulário adaptáveis. Essas regras definem as ações a serem acionadas nos objetos de formulário com base nas condições predefinidas, entradas do usuário e ações do usuário no formulário. Isso ajuda a simplificar ainda mais a experiência de preenchimento de formulário, garantindo precisão e velocidade.

O editor de regras fornece uma interface de usuário intuitiva e simplificada para escrever regras. O editor de regras oferece um editor visual para todos os usuários. Além disso, somente para usuários avançados de formulários, o editor de regras fornece um editor de código para escrever regras e scripts.
<!-- Some of the key actions that you can perform on adaptive form objects using rules are:

* Show or hide an object
* Enable or disable an object
* Set a value for an object
* Validate the value of an object
* Execute functions to compute the value of an object
* Invoke a form data model service and perform an operation
* Set property of an object -->

O Editor de regras substitui os recursos de script no AEM 6.1 Forms e em versões anteriores. No entanto, os scripts existentes são preservados no novo editor de regras. Para obter mais informações sobre como trabalhar com scripts existentes no editor de regras, consulte [Impacto do editor de regras nos scripts existentes](#impact-of-rule-editor-on-existing-scripts).

Os usuários adicionados ao grupo forms-power-users podem criar novos scripts e editar os existentes. Os usuários no grupo formulários-usuários podem usar os scripts, mas não criar ou editar scripts.

## Noções básicas sobre uma regra {#understanding-a-rule}

Uma regra é uma combinação de ações e condições. No editor de regras, as ações incluem atividades como ocultar, mostrar, habilitar, desabilitar ou calcular o valor de um objeto em um formulário. As condições são expressões booleanas que são avaliadas executando verificações e operações no estado, valor ou propriedade de um objeto de formulário. As ações são executadas com base no valor ( `True` ou `False`) retornado pela avaliação de uma condição.

O editor de regras fornece um conjunto de tipos de regras predefinidos, como Quando, Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar, para ajudá-lo a escrever regras. Cada tipo de regra permite definir condições e ações em uma regra. O documento explica detalhadamente cada tipo de regra.

Uma regra normalmente segue uma das seguintes construções:

**Condition-Action** Nesta construção, uma regra primeiro define uma condição seguida por uma ação a ser acionada. A construção é comparável à instrução if-then em linguagens de programação.

No editor de regras, o tipo de regra **When** impõe a construção de condição-ação.

**Condição-ação** Nesta construção, uma regra primeiro define uma ação a ser acionada seguida por condições para avaliação. Outra variação dessa construção é ação-condição-ação alternativa, que também define uma ação alternativa a ser acionada se a condição retornar Falso.

Os tipos de regras Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar no editor de regras impõem a construção de regra de condição de ação. Por padrão, a ação alternativa para Mostrar é Ocultar, e para Habilitar é Desabilitar e vice-versa. Não é possível alterar a ação alternativa padrão.

>[!NOTE]
>
>Os tipos de regras disponíveis, incluindo condições e ações definidas no editor de regras, também dependem do tipo de objeto de formulário no qual você está criando uma regra. O editor de regras exibe somente tipos de regras válidos e opções para gravar instruções de condição e ação para um determinado tipo de objeto de formulário. Por exemplo, você não vê os tipos de regras Validar, Definir valor de, Ativar e Desativar para um objeto de painel.

Para obter mais informações sobre tipos de regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](#available-rule-types-in-rule-editor).

### Diretrizes para a escolha de uma construção de regra {#guidelines-for-choosing-a-rule-construct}

Embora seja possível obter a maioria dos casos de uso usando qualquer construção de regra, veja a seguir algumas diretrizes para escolher uma construção em vez de outra. Para obter mais informações sobre as regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](#available-rule-types-in-rule-editor).

* Uma regra prática comum ao criar uma regra é pensar nela no contexto do objeto no qual você está escrevendo uma regra. Considere que deseja ocultar ou mostrar o campo B com base no valor especificado por um usuário no campo A. Nesse caso, você está avaliando uma condição no campo A e, com base no valor retornado, aciona uma ação no campo B.

  Portanto, se estiver escrevendo um regra no campo B (o objeto sobre o qual você está avaliando uma condição), use a construção de ação de condição ou o tipo Quando regra. Da mesma forma, use a construção de condição de ação ou Exibir ou oculte regra tipo no campo A.

* Às vezes, você precisa executar várias ações com base em uma condição. Nesses casos, recomenda-se usar a construção de ação condicional. Nesta construção, você pode avaliar uma condição uma vez e especificar várias declarações de ação.

  Por exemplo, para ocultar campos B, C e D com base na condição que verifica o valor que uma usuário especifica no campo A, escreva uma regra com construção de ação de condição ou Quando regra tipo no campo A e especifique ações para controlar a visibilidade dos campos B, C e D. Caso contrário, você precisa de três regras separadas nos campos B,  C e D, onde cada regra verifica a condição e mostra ou oculta o respectivo campo. Neste exemplo, é mais eficiente escrever o tipo Quando regra em um objeto em vez de Exibir ou Ocultar regra tipo em três objetos.

* Para acionar uma ação baseada em várias condições, recomenda-se usar a construção de condições de ação. Por exemplo, para mostrar e ocultar campo A avaliando as condições nos campos B, C e D, use Exibir ou Ocultar regra tipo no campo A.
* Use a construção de condição-ação ou condição de ação se a regra contiver uma ação para uma condição.
* Se uma regra verificar uma condição e executar uma ação imediatamente ao fornecer um valor em um campo ou ao sair de um campo, é recomendável gravar uma regra com construção de condição-ação ou o tipo de regra Quando no campo em que a condição é avaliada.
* A condição na regra Quando é avaliada quando um usuário altera o valor do objeto no qual a regra Quando é aplicada. No entanto, se você quiser que a ação seja acionada quando o valor for alterado no lado do servidor, como no preenchimento prévio do valor, é recomendável gravar uma regra When que aciona a ação quando o campo é inicializado.
* Ao escrever regras para objetos de menus suspensos, botões de opção ou caixas de seleção, as opções ou os valores desses objetos de formulário no formulário são preenchidos previamente no editor de regras.

## Tipos de operadores e eventos disponíveis no editor de regras {#available-operator-types-and-events-in-rule-editor}

O editor de regras fornece os seguintes operadores lógicos e eventos com os quais você pode criar regras.

* **É Igual A**
* **Não É Igual A**
* **Começa com**
* **Termina com**
* **Contém**
* **Está Vazio**
* **Não Está Vazio**
* **Selecionado:** Retorna verdadeiro quando o usuário seleciona uma opção específica para uma caixa de seleção, lista suspensa, botão de opção.
* **Inicializado (evento):** Retorna verdadeiro quando um objeto de formulário é renderizado no navegador.
* **Está Alterado (evento):** Retorna verdadeiro quando o usuário altera o valor inserido ou a opção selecionada para um objeto de formulário.

## Tipos de regras disponíveis no editor de regras {#available-rule-types-in-rule-editor}

O editor de regras fornece um conjunto de tipos de regras predefinidos que você pode usar para escrever regras. Vamos analisar cada tipo de regra detalhadamente. Para obter mais informações sobre como gravar regras no editor de regras, consulte [Regras de gravação](#write-rules).

### Quando {#whenruletype}

O tipo de regra **When** segue a construção de regra **ação-condição-ação-alternativa**, ou, às vezes, apenas a construção **ação-condição**. Nesse tipo de regra, primeiro especifique uma condição para avaliação seguida por uma ação para acionar se a condição for atendida ( `True`). Ao usar o tipo de regra When, você pode usar vários operadores AND e OR para criar [expressões aninhadas](#nestedexpressions).

Usando o tipo de regra Quando, é possível avaliar uma condição em um objeto de formulário e executar ações em um ou mais objetos.

Em palavras simples, uma regra When típica é estruturada da seguinte maneira:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Ação 2 no objeto B;
E
Ação 3 no Objeto C;

_

Quando você tem um componente de vários valores, como botões de opção ou lista, ao criar uma regra para esse componente, as opções são automaticamente recuperadas e disponibilizadas para o criador da regra. Não é necessário digitar os valores da opção novamente.

Por exemplo, uma lista tem quatro opções: Vermelho, Azul, Verde e Amarelo. Ao criar a regra, as opções (botões de opção) são recuperadas automaticamente e disponibilizadas ao criador da regra da seguinte maneira:

![multivaluefcdisplaysoptions](assets/multivaluefcdisplaysoptions.png)

Ao escrever uma regra Quando, é possível acionar a ação Limpar valor de. Limpar valor da ação limpa o valor do objeto especificado. Ter o valor claro de como uma opção na instrução When permite criar condições complexas com vários campos.

![clearvalueof](assets/clearvalueof.png)

**Ocultar** oculta o objeto especificado.

**Mostrar** Mostra o objeto especificado.

**Habilitar** Habilita o objeto especificado.

**Desabilitar** Desabilita o objeto especificado.

**Invocar serviço** Invoca um serviço configurado em um modelo de dados de formulário. Quando você escolhe a operação Chamar Serviço, um campo é exibido. Ao tocar no campo, ele exibe todos os serviços configurados em todos os modelos de dados de formulário na instância do AEM. Ao escolher um serviço de modelo de dados de formulário, campos adicionais são exibidos onde você pode mapear objetos de formulário com parâmetros de entrada e saída para o serviço especificado. Consulte exemplo de regra para chamar serviços de modelo de dados de formulário.

Além do serviço de modelo de dados de formulário, você pode especificar um URL WSDL direto para chamar um serviço Web. No entanto, um serviço de modelo de dados de formulário tem muitos benefícios e a abordagem recomendada para chamar um serviço.

Para obter mais informações sobre como configurar serviços no modelo de dados de formulário, consulte [Integração de Dados do AEM Forms](/help/forms/using/data-integration.md).

**Defina o valor de** Computes e defina o valor do objeto especificado. Você pode definir o valor do objeto como uma string, o valor de outro objeto, o valor calculado usando expressão matemática ou função, o valor de uma propriedade de um objeto ou o valor de saída de um serviço de modelo de dados de formulário configurado. Quando você escolhe a opção de serviço da Web, ela exibe todos os serviços configurados em todos os modelos de dados de formulário na sua instância do AEM. Ao escolher um serviço de modelo de dados de formulário, campos adicionais são exibidos onde você pode mapear objetos de formulário com parâmetros de entrada e saída para o serviço especificado.

Para obter mais informações sobre como configurar serviços no modelo de dados de formulário, consulte [Integração de Dados do AEM Forms](/help/forms/using/data-integration.md).

O tipo de regra **[!UICONTROL Definir Propriedade]** permite que você defina o valor de uma propriedade do objeto especificado com base em uma ação de condição. Você pode definir a propriedade como uma das seguintes opções:

* visível (Booleano)
* dorExclusion (Booleano)
* chartType (String)
* título (String)
* ativado (Booleano)
* obrigatório (booleano)
* validationsDisabled (Booleano)
* validateExpMessage (String)
* value (Número, String, Data)
* itens (Lista)
* válido (Booleano)
* errorMessage (String)

Ela permite definir regras para adicionar caixas de seleção dinamicamente ao formulário adaptável. Você pode usar uma função personalizada, um objeto de formulário ou uma propriedade de objeto para definir uma regra.

![Definir Propriedade](assets/set_property_rule_new.png)

Para definir uma regra com base em uma função personalizada, selecione **Saída da Função** na lista suspensa e arraste e solte uma função personalizada na guia **Funções**. Se a ação de condição for atendida, o número de caixas de seleção definidas na função personalizada será adicionado ao formulário adaptável.

Para definir uma regra baseada em um objeto de formulário, selecione **Objeto de formulário** na lista suspensa e arraste e solte um objeto de formulário da guia **Objetos de formulário**. Se a ação de condição for atendida, o número de caixas de seleção definidas no objeto de formulário será adicionado ao formulário adaptável.

Uma regra Definir propriedade com base em uma propriedade de objeto permite adicionar o número de caixas de seleção em um formulário adaptável com base em outra propriedade de objeto incluída no formulário adaptável.

A figura a seguir mostra um exemplo de adição dinâmica de caixas de seleção com base no número de listas suspensas no formulário adaptável:

![Propriedade do objeto](assets/object_property_set_property_new.png)

**Limpar Valor de** Limpa o valor do objeto especificado.

**Definir Foco** Define o foco no objeto especificado.

**Salvar formulário** Salva o formulário.

**Enviar Forms** Envia o formulário.

**Redefinir formulário** Redefine o formulário.

**Validar formulário** Valida o formulário.

**Adicionar instância** Adiciona uma instância do painel ou linha de tabela repetível especificado.

**Remover instância** Remove uma instância do painel ou linha de tabela repetível especificado.

**Navegar até** Navega até outras Comunicações interativas, formulários adaptáveis, outros ativos, como imagens ou fragmentos de documentos, ou uma URL externa. Para obter mais informações, consulte [Adicionar botão à Comunicação Interativa](../../forms/using/create-interactive-communication.md#addbuttontothewebchannel).

### Definir valor de {#set-value-of}

O tipo de regra **[!UICONTROL Definir Valor de]** permite que você defina o valor de um objeto de formulário, dependendo se a condição especificada é atendida ou não. O valor pode ser definido como um valor de outro objeto, uma string literal, um valor derivado de uma expressão matemática ou de uma função, um valor de uma propriedade de outro objeto ou a saída de um serviço de modelo de dados de formulário. Da mesma forma, você pode verificar uma condição em um componente, string, propriedade ou valores derivados de uma função ou expressão matemática.

O tipo de regra Definir valor de não está disponível para todos os objetos de formulário, como painéis e botões da barra de ferramentas. Uma regra padrão Definir valor de tem a seguinte estrutura:



Defina o valor do Objeto A como:

(cadeia de caracteres ABC) OU
(propriedade de objeto X do Objeto C) OU
(valor de uma função) OR
(valor de uma expressão matemática) OR
(valor de saída de um serviço de modelo de dados ou serviço Web);

Quando (opcional):

(Condição 1 E Condição 2 E Condição 3) é VERDADEIRA;



O exemplo a seguir usa o valor em `dependentid` campo como entrada e define o `Relation` valor do campo para a saída do `Relation` argumento do serviço de modelo de dados de `getDependent` formulário.

![set-value-web-service](assets/set-value-web-service.png)

Exemplo de regra Definir valor usando o serviço de modelo de dados de formulário

>[!NOTE]
>
>Além disso, você pode usar Definir valor da regra para preencher todos os valores em um componente de lista suspensa a partir da saída de um serviço de modelo de dados de formulário ou um serviço Web. No entanto, verifique se o argumento de saída escolhido é de um tipo de matriz. Todos os valores retornados em uma matriz ficam disponíveis na lista suspensa especificada.

### Mostrar {#show}

Usando o tipo de regra **Mostrar**, você pode escrever uma regra para mostrar ou ocultar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Mostrar também aciona a ação Ocultar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de exibição está estruturada da seguinte maneira:



`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`



### Ocultar {#hide}

Semelhante ao tipo de regra Mostrar, você pode usar o tipo de regra **Ocultar** para mostrar ou ocultar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Ocultar também aciona a ação Mostrar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de Ocultar está estruturada da seguinte maneira:



`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`



### Habilitar {#enable}

O tipo de regra **Habilitar** permite habilitar ou desabilitar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Habilitar também aciona a ação Desabilitar caso a condição não seja atendida ou retorne `False`.

Uma regra Enable típica é estruturada da seguinte maneira:



`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`



### Desativar {#disable}

Semelhante ao tipo de regra Habilitar, o tipo de regra **Desabilitar** permite habilitar ou desabilitar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Desativar também aciona a ação Ativar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de Desativação está estruturada da seguinte maneira:



`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### Validar {#validate}

O tipo de regra **Validar** valida o valor em um campo usando uma expressão. Por exemplo, você pode escrever uma expressão para verificar se a caixa de texto para especificar o nome não contém caracteres especiais ou números.

Uma regra Validate típica é estruturada da seguinte maneira:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se o valor especificado não estiver em conformidade com a regra Validar, você poderá exibir uma mensagem de validação para o usuário. Você pode especificar a mensagem no campo **[!UICONTROL Mensagem de validação de script]** nas propriedades do componente na barra lateral.

![validação-script](assets/script-validation.png)

### Definir Opções De {#setoptionsof}

O tipo de regra **Definir Opções de** permite que você defina regras para adicionar caixas de seleção dinamicamente ao formulário adaptável. Você pode usar um modelo de dados de formulário ou uma função personalizada para definir a regra.

Para definir uma regra com base em uma função personalizada, selecione **Saída da Função** na lista suspensa e arraste e solte uma função personalizada na guia **Funções**. O número de caixas de seleção definidas na função personalizada é adicionado ao formulário adaptável.

![Funções personalizadas](assets/custom_functions_set_options_new.png)

Para criar uma função personalizada, consulte [funções personalizadas no editor de regras](#custom-functions).

Para definir uma regra baseada em um modelo de dados de formulário:

1. Selecione **Saída de Serviço** na lista suspensa.
1. Selecione o objeto de modelo de dados.
1. Selecione uma propriedade de objeto de modelo de dados na lista suspensa **Valor de Exibição**. O número de caixas de seleção no formulário adaptável é derivado do número de instâncias definidas para essa propriedade no banco de dados.
1. Selecione uma propriedade de objeto de modelo de dados na lista suspensa **Salvar Valor**.

![Opções de conjunto de FDM](assets/fdm_set_options_new.png)

## Noções básicas sobre a interface do usuário do editor de regras {#understanding-the-rule-editor-user-interface}

O Editor de regras fornece uma interface de usuário abrangente, mas simples, para gravar e gerenciar regras. É possível iniciar a interface do usuário do editor de regras a partir de um formulário adaptável no modo de criação.

Para iniciar a interface do usuário do editor de regras:

1. Abra um formulário adaptável no modo de criação.
1. Selecione o objeto de formulário para o qual deseja gravar uma regra e, na Barra de Ferramentas do Componente, selecione ![edit-rules](assets/edit-rules.png). A interface do usuário do editor de regras é exibida.

   ![criar-regras](assets/create-rules.png)

   Todas as regras existentes nos objetos de formulário selecionados são listadas nessa exibição. Para obter informações sobre como gerenciar regras existentes, consulte [Gerenciar regras](#manage-rules).

1. Selecione **[!UICONTROL Criar]** para escrever uma nova regra. O editor visual da interface do usuário do editor de regras é aberto por padrão quando você inicia o editor de regras pela primeira vez.

   ![Interface do Editor de Regras](assets/rule-editor-ui.png)

Vamos analisar cada componente da interface do editor de regras em detalhes.

### A. Exibição de componente-regra {#a-component-rule-display}

Exibe o título do objeto de formulário adaptável pelo qual você iniciou o editor de regras e o tipo de regra selecionado no momento. No exemplo acima, o editor de regras é iniciado a partir de um objeto de formulário adaptável chamado Salário, e o tipo de regra selecionado é Quando.

### B. Funções e objetos de formulário {#b-form-objects-and-functions-br}

O painel à esquerda na interface do usuário do editor de regras inclui duas guias: **[!UICONTROL Objetos do Forms]** e **[!UICONTROL Funções]**.

A guia Objetos de formulário mostra uma exibição hierárquica de todos os objetos contidos no formulário adaptável. Ele exibe o título e o tipo dos objetos. Ao escrever uma regra, você pode arrastar e soltar objetos de formulário no editor de regras. Ao criar ou editar uma regra ao arrastar e soltar um objeto ou função em um espaço reservado, o espaço reservado automaticamente assume o tipo de valor apropriado.

Os objetos de formulário que têm uma ou mais regras válidas aplicadas são marcados com um ponto verde. Se alguma das regras aplicadas a um objeto de formulário for inválida, o objeto de formulário será marcado com um ponto amarelo.

As Funções guia incluem um conjunto de funções integradas, como Soma de, Mín, Máx. de, Média, Número e Formulário validado. Você pode usar essas funções para calcular valores em painéis e linhas de tabela repetíveis e usá-los em declarações de ação e condição ao escrever regras. No entanto, também é possível criar [funções personalizadas](#custom-functions) .

![As funções guia](assets/functions.png)

>[!NOTE]
>
>Você pode executar a pesquisa de texto em nomes de objetos e funções e títulos nas guias Objetos e Funções do Forms.

Na árvore esquerda dos objetos de formulário, você pode selecionar os objetos de formulário para exibir as regras aplicadas a cada um dos objetos. Você não só pode navegar pelas regras dos vários objetos de formulário, como também pode copiar e colar regras entre os objetos de formulário. Para obter mais informações, consulte [Copiar-colar regras](#copy-paste-rules).

### C. Alternância entre objetos e funções de formulário {#c-form-objects-and-functions-toggle-br}

O botão de alternância, quando tocado, alterna o painel de funções e objetos de formulário.

### D. Editor visual de regras {#d-visual-rule-editor}

Editor visual de regras é a área no modo editor visual da interface do usuário do editor de regras em que você escreve regras. Ele permite selecionar um tipo de regra e definir adequadamente condições e ações. Ao definir condições e ações em uma regra, você pode arrastar e soltar objetos e funções de formulário do painel Objetos de formulário e Funções.

Para obter mais informações sobre como usar o editor visual de regras, consulte [Regras de gravação](#write-rules).

### E. Seletor de editores de código visual {#e-visual-code-editors-switcher}

Os usuários no grupo forms-power-users podem acessar o editor de código. Para outros usuários, o editor de código não está disponível. Se você tiver os direitos, poderá alternar do modo do editor visual para o modo do editor de códigos do editor de regras e vice-versa, usando o alternador logo acima do editor de regras. Quando você inicia o editor de regras pela primeira vez, ele é aberto no modo do editor visual. Você pode escrever regras no modo de editor visual ou alternar para o modo de editor de código para escrever um script de regra. No entanto, observe que, se você modificar uma regra ou escrevê-la no editor de códigos, não poderá voltar para o editor visual dessa regra, a menos que o editor de códigos seja limpo.

O AEM Forms rastreia o modo do editor de regras usado por último para escrever uma regra. Na próxima vez que você iniciar o editor de regras, ele será aberto nesse modo. No entanto, também é possível configurar um modo padrão para abrir o editor de regras no modo especificado. Para fazer isso:

1. Ir para o console da Web do AEM em `https://[host]:[port]/system/console/configMgr`.
1. Clique para editar **[!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa]**.
1. escolha **[!UICONTROL Editor Visual]** ou **[!UICONTROL Editor de Código]** no menu suspenso **[!UICONTROL Modo Padrão do Editor de Regras]**

1. Clique em **[!UICONTROL Salvar]**.

### F. Botões Concluído e Cancelar {#f-done-and-cancel-buttons}

O botão **[!UICONTROL Concluído]** é usado para salvar uma regra. Você pode salvar uma regra incompleta. No entanto, incompletos são inválidos e não são executados. As regras salvas em um objeto de formulário são listadas na próxima vez que você iniciar o editor de regras a partir do mesmo objeto de formulário. Você pode gerenciar as regras existentes nessa visualização. Para obter mais informações, consulte [Gerenciar regras](#manage-rules).

O botão **[!UICONTROL Cancelar]** descarta todas as alterações feitas em uma regra e fecha o editor de regras.

## Regras de gravação {#write-rules}

É possível escrever regras usando o editor visual de regras ou o editor de códigos. Quando você inicia o editor de regras pela primeira vez, ele é aberto no modo do editor visual. Você pode alternar para o modo do editor de código e escrever regras. No entanto, observe que, se você escrever ou modificar uma regra no editor de códigos, não poderá alternar para o editor visual dessa regra, a menos que o editor de códigos seja limpo. Na próxima vez que você iniciar o editor de regras, ele será aberto no modo usado por último para criar a regra.

Primeiro, vamos analisar como escrever regras usando o editor visual.

### Uso do editor visual {#using-visual-editor}

Vamos entender como criar uma regra no editor visual usando o seguinte formulário de exemplo.

![criar-regra-exemplo](assets/create-rule-example.png)

A seção Requisitos de Empréstimo no formulário de solicitação de empréstimo de exemplo exige que os candidatos especifiquem seu estado civil, salário e, se forem casados, o salário de seus cônjuges. Com base nas entradas do usuário, a regra calcula o valor de qualificação de empréstimo e é exibida no campo Elegibilidade do empréstimo. Aplique as seguintes regras para implementar o cenário:

* O campo Salário do Cônjuge é exibido somente quando o Estado Civil é Casado.
* O valor de qualificação de empréstimo é de 50% do salário total.

Execute as seguintes etapas para escrever regras:

1. Primeiro, escreva a regra para controlar a visibilidade do campo Salário do Cônjuge com base na opção que o usuário seleciona para o botão de opção Estado Civil.

   Abra o formulário de solicitação de empréstimo no modo de criação. Selecione o componente **Estado civil** e selecione ![edit-rules](assets/edit-rules.png). Em seguida, selecione **[!UICONTROL Criar]** para iniciar o editor de regras.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Ao iniciar o editor de regras, a regra Quando é selecionada por padrão. Além disso, o objeto de formulário (nesse caso, Estado civil) de onde você iniciou o editor de regras é especificado na instrução When.

   Embora não seja possível alterar ou modificar o objeto selecionado, você poderá usar o menu suspenso de regras, como mostrado abaixo, para selecionar outro tipo de regra. Se quiser criar uma regra em outro objeto, selecione Cancelar para sair do editor de regras e iniciá-lo novamente a partir do objeto de formulário desejado.

1. Selecione o menu suspenso **[!UICONTROL Selecionar estado]** e selecione **[!UICONTROL é igual a]**. O campo **[!UICONTROL Inserir uma cadeia de caracteres]** é exibido.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   No botão de opção Estado Civil, as opções **Casado** e **Único** recebem os valores **0** e **1**, respectivamente. Você pode verificar os valores atribuídos na guia Título da caixa de diálogo Editar botão de opção, conforme mostrado abaixo.

   ![Valores do botão de opção do editor de regras](assets/radio-button-values.png)

1. No campo **Inserir uma Cadeia de Caracteres** na regra, especifique **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   Você definiu a condição como `When Marital Status is equal to Married`. Em seguida, defina a ação a ser executada se essa condição for True.

1. Na instrução Then, selecione **[!UICONTROL Mostrar]** no menu suspenso **[!UICONTROL Selecionar Ação]**.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Arraste e solte o campo **Salário do Cônjuge** da guia Objetos de Formulário no campo **Soltar objeto ou selecionar aqui**. Como alternativa, selecione o campo **Soltar objeto ou selecione aqui** e selecione o campo **Salário do Cônjuge** no menu pop-up, que lista todos os objetos de formulário no formulário.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   A regra é exibida da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

   Selecione **Concluído** para salvar a regra.

1. Repita as etapas de 1 a 5 para definir outra regra para ocultar o campo Salário do Cônjuge se o estado civil for Simples. A regra é exibida da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >Como alternativa, você pode escrever uma regra Mostrar no campo Salário do Cônjuge, em vez de duas regras Quando no campo Estado Civil, para implementar o mesmo comportamento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Em seguida, escreva uma regra para calcular o valor de qualificação de empréstimo, que é 50% do salário total, e exiba-o no campo Elegibilidade do empréstimo. Para fazer isso, crie **Definir valor de** regras no campo Elegibilidade para empréstimo.

   No modo de criação, selecione o campo **[!UICONTROL Qualificação para empréstimo]** e selecione ![edit-rules](assets/edit-rules.png). Em seguida, selecione **[!UICONTROL Criar]** para iniciar o editor de regras.

1. Selecione a regra **[!UICONTROL Definir Valor de]** no menu suspenso de regras.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Selecione **[!UICONTROL Selecionar Opção]** e selecione **[!UICONTROL Expressão Matemática]**. Um campo para escrever expressão matemática é aberto.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. No campo de expressão:

   * Selecione ou arraste e solte da guia Objeto do Forms o campo **Salário** no primeiro campo **Soltar objeto ou selecione aqui**.

   * Selecione **Plus** no campo **Selecionar Operador**.

   * Selecione ou arraste e solte na guia Objeto do Forms o campo **Salário do Cônjuge** no outro objeto **Solte ou selecione aqui**.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Em seguida, selecione na área destacada ao redor do campo de expressão e selecione **Estender expressão**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   No campo de expressão estendida, selecione **dividido por** no campo **Selecionar Operador** e **Número** no campo **Selecionar Opção**. Em seguida, especifique **2** no campo de número.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >Você pode criar expressões complexas usando componentes, funções, expressões matemáticas e valores de propriedade no campo Selecionar opção.

   Em seguida, crie uma condição, que quando retorna True, a expressão é executada.

1. Selecione **Adicionar Condição** para adicionar uma instrução When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Na instrução When:

   * Selecione ou arraste e solte na guia Objeto do Forms o campo **Estado civil** no primeiro campo **Soltar objeto ou selecione aqui**.

   * Selecione i **s igual a** no campo **Selecionar Operador**.

   * Selecione a string no outro objeto **Soltar ou selecione aqui** e especifique **Casado** no campo **Inserir uma string**.

   A regra finalmente aparece da seguinte maneira no editor de regras.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

   Selecione **Concluído** para salvar a regra.

1. Repita as etapas 7 a 12 para definir outra regra para calcular a elegibilidade do empréstimo se o estado civil for Simples. A regra é exibida da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>Como alternativa, você pode usar a regra Definir Valor de para calcular a elegibilidade do empréstimo na regra Quando criada para mostrar/ocultar o campo Salário do Cônjuge. A regra combinada resultante quando o estado civil é Simples é exibida da seguinte maneira no editor de regras.
>
>Da mesma forma, você pode escrever uma regra combinada para controlar a visibilidade do campo Salário do Cônjuge e calcular a elegibilidade para empréstimo quando o estado civil é Casado.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

### Uso do editor de código {#using-code-editor}

Os usuários adicionados ao grupo forms-power-users podem usar o editor de código. O editor de regras gera automaticamente o código JavaScript para qualquer regra criada usando o editor visual. Você pode alternar do editor visual para o editor de código para exibir o código gerado. No entanto, se você modificar o código da regra no editor de código, não poderá voltar para o editor visual. Se preferir escrever regras no editor de código em vez do editor visual, você pode escrever regras novamente no editor de código. O alternador de editores de código visual ajuda você a alternar entre os dois modos.

O editor de código JavaScript é a linguagem de expressão de formulários adaptáveis. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de determinados tipos. Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/br/experience-manager/6-5/forms/javascript-api/index.html).

Para obter mais informações sobre diretrizes para escrever regras no editor de código, consulte [Expressões de formulários adaptáveis](/help/forms/using/adaptive-form-expressions.md).

Ao escrever o código JavaScript no editor de regras, as seguintes dicas visuais ajudam na estrutura e na sintaxe:

* Destaques da sintaxe
* Recuo Automático
* Dicas e sugestões para objetos de formulário, funções e suas propriedades
* Preenchimento automático de nomes de componentes de formulário e funções comuns do JavaScript

![javascriptruleeditor](assets/javascriptruleeditor.png)

#### Funções personalizadas no editor de regras {#custom-functions}

Além das funções prontas para uso como *Soma de* que estão listadas em Saída de funções, você pode gravar funções personalizadas das quais precisa com frequência. Certifique-se de que a função que você grava esteja acompanhada pelo `jsdoc` acima dela.

O acompanhamento de `jsdoc` é obrigatório:

* Se desejar configuração e descrição personalizadas.
* Como há várias maneiras de declarar uma função em `JavaScript,`, os comentários permitem que você acompanhe as funções.

Para obter mais informações, consulte [usejsdoc.org](https://jsdoc.app/).

`jsdoc` marcas com suporte:

* **Particular**
Sintaxe: `@private`
Uma função privada não está incluída como uma função personalizada.

* **Nome**
Sintaxe: `@name funcName <Function Name>`
Alternativamente, o `,` é possível usar o `@function funcName <Function Name>` **ou o** `@func` `funcName <Function Name>`.
  `funcName` é o nome da função (nenhum espaço é permitido).
  `<Function Name>` é o nome para exibição da função.

* **Membro**
Sintaxe: `@memberof namespace`
Anexa um namespace à função.

* **Parâmetro**
Sintaxe: `@param {type} name <Parameter Description>`
Como alternativa, você pode usar: `@argument` `{type} name <Parameter Description>` **ou** `@arg` `{type}` `name <Parameter Description>`.
Mostra os parâmetros usados pela função. Uma função pode ter várias tags de parâmetro, uma tag para cada parâmetro na ordem de ocorrência.
  `{type}` representa o tipo de parâmetro. Os tipos de parâmetros permitidos são:

   1. string
   1. número
   1. booleano
   1. escopo

  O escopo é usado para campos de referência de um Formulário adaptável. Quando um formulário usa carregamento lento, você pode usar `scope` para acessar seus campos. Você pode acessar campos quando eles forem carregados ou se estiverem marcados como globais.

  Todos os outros tipos de parâmetros são categorizados em um dos acima. Nenhum não é compatível. Selecione um dos tipos acima. Os tipos não diferenciam maiúsculas de minúsculas. Não são permitidos espaços no parâmetro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo de Retorno**
Sintaxe: `@return {type}`
Como alternativa, você pode usar `@returns {type}`.
Adiciona informações sobre a função, como seu objetivo.
{type} representa o tipo de retorno da função. Os tipos de retorno permitidos são:

   1. string
   1. número
   1. booleano

  Todos os outros tipos de retorno são categorizados em um dos itens acima. Nenhum não é compatível. Selecione um dos tipos acima. Os tipos de retorno não diferenciam maiúsculas de minúsculas.

* **Isto**
Sintaxe: `@this currentComponent`

  Use @this para se referir ao componente de Formulário adaptável no qual a regra é gravada.

  O exemplo a seguir é baseado no valor do campo. No exemplo a seguir, a regra oculta um campo no formulário. A parte `this` de `this.value` refere-se ao componente de Formulário adaptável subjacente, no qual a regra é gravada.

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function will be executed.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

>[!NOTE]
>
>Comentários antes da função personalizada são usados para resumo. O resumo pode ser estendido para várias linhas até que uma tag seja encontrada. Limite o tamanho a um único para obter uma descrição concisa no construtor de regras.

<!--
**Adding a custom function**

For example, you want to add a custom function which calculates area of a square. Side length is the user input to the custom function, which is accepted using a numeric box in your form. The calculated output is displayed in another numeric box in your form. To add a custom function, you have to first create a client library, and then add it to the CRX repository.

Perform the following steps to create a client library and add it in the CRX repository.

1. Create a client library. For more information, see [Using Client-Side Libraries](/help/sites-developing/clientlibs.md).
2. In CRXDE, add a property `categories`with string type value as `customfunction` to the `clientlib` folder.

   >[!NOTE]
   >
   >`customfunction`is an example category. You can choose any name for the category you create in the `clientlib`folder.

After you have added your client library in the CRX repository, use it in your adaptive form. It lets you use your custom function as a rule in your form. Perform the following steps to add the client library in your adaptive form.

1. Open your form in edit mode.
   To open a form in edit mode, select a form and select **Open**.
1. In the edit mode, select a component, then select ![field-level](assets/field-level.png) &gt; **Adaptive Form Container**, and then select ![cmppr](assets/cmppr.png).
1. In the sidebar, under Name of Client Library, add your client library. ( `customfunction` in the example.)

   ![Adding the custom function client library](assets/clientlib.png)

1. Select the input numeric box, and select ![edit-rules](assets/edit-rules.png) to open the rule editor.
1. Select **Create Rule**. Using options shown below, create a rule to save the squared value of the input in the Output field of your form.
   [ ![Using custom functions to create a rule](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)Select **Done**. Your custom function is added.

#### Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Ensure that you use `jsdoc` for every custom function. Although `jsdoc`comments are encouraged, include an empty `jsdoc`comment to mark your function as custom function. It enables default handling of your custom function.
-->

Também é possível usar funções personalizadas no editor de regras. Para obter instruções sobre como criar funções personalizadas, consulte o artigo [Funções personalizadas no Adaptive Forms](/help/forms/using/create-and-use-custom-functions.md).

## Gerenciar regras {#manage-rules}

Todas as regras existentes em um objeto de formulário são listadas ao selecionar o objeto e selecionar ![edit-rules1](assets/edit-rules1.png). É possível exibir o título e uma pré-visualização do resumo da regra. Além disso, a interface do permite expandir e exibir o resumo completo da regra, alterar a ordem das regras, editar regras e excluir regras.

![regras-lista](assets/list-rules.png)

Você pode executar as seguintes ações nas regras:

* **Expandir/Recolher**: a coluna Conteúdo da lista de regras exibe o conteúdo da regra. Se o conteúdo inteiro da regra não estiver visível no modo de exibição padrão, selecione ![expand-rule-content](assets/expand-rule-content.png) para expandi-lo.

* **Reordenar**: qualquer nova regra criada é empilhada na parte inferior da lista de regras. As regras são executadas de cima para baixo. A regra na parte superior é executada primeiro, seguida por outras regras do mesmo tipo. Por exemplo, se você tiver regras When, Show, Enable e When na primeira, segunda, terceira e quarta posições a partir da parte superior, respectivamente, a regra When na parte superior será executada primeiro, seguida pela regra When na quarta posição. Em seguida, as regras Show e Enable serão executadas.
Você pode alterar a ordem de uma regra tocando em ![sort-rules](assets/sort-rules.png) ou arrastando-a e soltando-a na ordem desejada na lista.

* **Editar**: para editar uma regra, marque a caixa de seleção ao lado do título da regra. São exibidas opções adicionais para editar e excluir a regra. Selecione **Editar** para abrir a regra selecionada no editor de regras no modo visual ou de editor de códigos, dependendo do modo usado para criar a regra.

* **Excluir**: para excluir uma regra, selecione a regra e selecione **Excluir**.

* **Habilitar/Desabilitar**: talvez seja necessário suspender o uso de uma regra temporariamente. É possível selecionar uma ou mais regras e selecionar Desativar na barra de ferramentas Ações para desativá-las. Se uma regra estiver desativada, ela não será executada no tempo de execução. Para habilitar uma regra que esteja desabilitada, você pode selecioná-la e selecionar Habilitar na barra de ferramentas de ações. A coluna de status da regra exibe se a regra está ativada ou desativada.

![regra de desabilitação](assets/disablerule.png)

## Copiar e colar regras {#copy-paste-rules}

É possível copiar e colar uma regra de um campo para outros campos semelhantes para economizar tempo.

Para copiar e colar regras, faça o seguinte:

1. Selecione o objeto de formulário do qual deseja copiar uma regra e, na barra de ferramentas do componente, selecione ![editar regra](assets/editrule.png). A interface do usuário do editor de regras é exibida com o objeto de formulário selecionado e as regras existentes são exibidas.

   ![copyrule](assets/copyrule.png)

   Para obter informações sobre como gerenciar regras existentes, consulte [Gerenciar regras](#manage-rules).

1. Marque a caixa de seleção ao lado do título da regra. São exibidas opções adicionais para gerenciar a regra. Selecione **Copiar**.

   ![copyrule2](assets/copyrule2.png)

1. Selecione outro objeto de formulário no qual você deseja colar a regra e selecione **Colar**. Além disso, você pode editar a regra para alterá-la.

   >[!NOTE]
   >
   >Você só poderá colar uma regra em outro objeto de formulário se esse objeto der suporte ao evento da regra copiada. Por exemplo, um botão oferece suporte ao evento click. É possível colar uma regra com um evento de clique em um botão, mas não em uma caixa de seleção.

1. Selecione **Concluído** para salvar a regra.

## Expressões aninhadas {#nestedexpressions}

O editor de regras permite usar vários operadores AND e OR para criar regras aninhadas. Você pode misturar vários operadores AND e OR em regras.

Veja a seguir um exemplo de uma regra aninhada que exibe uma mensagem ao usuário sobre a elegibilidade para a custódia de uma criança quando as condições necessárias são atendidas.

![complexexpression](assets/complexexpression.png)

Também é possível arrastar e soltar condições em uma regra para editá-la. Selecione e passe o mouse sobre o identificador ( ![identificador](assets/handle.png)) antes de uma condição. Depois que o ponteiro se transformar no símbolo da mão, como mostrado abaixo, arraste e solte a condição em qualquer lugar dentro da regra. A estrutura da regra muda.

![arrastar e soltar](assets/drag-and-drop.png)

## Condições de expressão de data {#dateexpression}

O editor de regras permite usar comparações de datas para criar condições.

A seguir está um exemplo de condição que exibe um objeto de texto estático se a hipoteca da casa já estiver sendo feita, o que o usuário significa preenchendo o campo de data.

Quando a data de hipoteca do imóvel conforme preenchido pelo usuário estiver no passado, o formulário adaptável exibe uma nota sobre o cálculo de renda. A regra a seguir compara a data preenchida pelo usuário com a data atual e, se a data preenchida pelo usuário for anterior à data atual, o formulário exibirá a mensagem de texto (chamada de Receita).

![dateexpressioncondition](assets/dateexpressioncondition.png)

Quando a data de preenchimento for anterior à data atual, o formulário exibirá a mensagem de texto (Receita) como a seguir:

![dateexpressionconditionmet](assets/dateexpressionconditionmet.png)

## Condições de comparação de número {#number-comparison-conditions}

O editor de regras permite criar condições que comparam dois números.

Veja a seguir um exemplo de condição que exibe um objeto de texto estático se o número de meses em que um candidato está hospedado em seu endereço atual for inferior a 36.

![numbercomparisoncondition](assets/numbercomparisoncondition.png)

Se o utilizador indicar que vive no seu endereço residencial atual há menos de 36 meses, o formulário contém uma notificação de que pode ser solicitada prova de residência adicional.

![aditionalproofrequested](assets/additionalproofrequested.png)

## Impacto do editor de regras nos scripts existentes {#impact-of-rule-editor-on-existing-scripts}

Nas versões do AEM Forms anteriores ao AEM 6.1 Forms feature pack 1, os autores e desenvolvedores de formulário costumavam escrever expressões na guia Scripts da caixa de diálogo Editar componente para adicionar comportamento dinâmico a formulários adaptáveis. A guia Scripts agora é substituída pelo editor de regras.

Todos os scripts ou expressões que você deve ter escrito na guia Scripts estão disponíveis no editor de regras. Embora não seja possível visualizá-los ou editá-los no editor visual, se você fizer parte do grupo de formulários-usuários avançados, será possível editar scripts no editor de código.

## Exemplo de regras {#example}

### Chamar serviço de modelo de dados de formulário {#invoke}

Considere um serviço Web `GetInterestRates` que obtém o valor do empréstimo, a estabilidade e a pontuação de crédito do candidato como entrada e retorna um plano de empréstimo incluindo o valor da IME e a taxa de juros. Crie um modelo de dados de formulário usando o serviço Web como uma fonte de dados. Você adiciona objetos de modelo de dados e um serviço `get` ao modelo de formulário. O serviço aparece na guia Serviços do modelo de dados de formulário. Em seguida, crie um formulário adaptável que inclua campos de objetos de modelo de dados para capturar as entradas do usuário para valor do empréstimo, estabilidade e pontuação de crédito. Adicione um botão que aciona o serviço Web para buscar detalhes do plano. A saída é preenchida nos campos apropriados.

A regra a seguir mostra como você configurará a ação Chamar serviço para realizar o cenário de exemplo.

![exemplo-invocar-serviços](assets/example-invoke-services.png)

Invocar o serviço de modelo de dados de formulário usando a regra de formulário adaptável

>[!NOTE]
>
>Se a entrada for do tipo matriz, os campos compatíveis com matrizes estarão visíveis na seção suspensa Saída.

### Acionamento de várias ações usando a regra Quando {#triggering-multiple-actions-using-the-when-rule}

Em um formulário de solicitação de empréstimo, você deseja registrar se o candidato ao empréstimo é um cliente existente ou não. Com base nas informações fornecidas pelo usuário, o campo ID do cliente deve mostrar ou ocultar. Além disso, é possível definir o foco no campo ID do cliente se o usuário for um cliente existente. O formulário de pedido de empréstimo tem os seguintes componentes:

* Um botão de opção, **Você já é cliente do Geometrixx?**, que fornece as opções Sim e Não. O valor de Sim é **0** e Não é **1**.

* Geometrixx Um campo de texto, **ID do cliente**, para especificar a ID do cliente.

Quando você escreve uma regra Quando no botão de opção para implementar esse comportamento, a regra é exibida da seguinte maneira no editor visual de regras.  ![quando-regra-exemplo](assets/when-rule-example.png)

Regra no editor visual

Na regra de exemplo, a instrução na seção When é a condição, que quando retorna True, executa as ações especificadas na seção Then.

A regra é exibida da seguinte maneira no editor de código.

![quando-regra-exemplo-código](assets/when-rule-example-code.png)

Regra no editor de código

### Uso de uma saída de função em uma regra {#using-a-function-output-in-a-rule}

Em um formulário de ordem de compra, você tem a tabela a seguir, na qual os usuários preencherão seus pedidos. Nesta tabela:

* A primeira linha pode ser repetida, para que os usuários possam solicitar vários produtos e especificar quantidades diferentes. Seu nome de elemento é `Row1`.
* O título da célula na coluna Quantidade do Produto da linha repetível é Quantidade. O nome do elemento desta célula é `productquantity`.
* A segunda linha da tabela não pode ser repetida e o título da célula na coluna Quantidade do Produto nesta linha é Quantidade Total.

![exemplo-tabela-função](assets/example-function-table.png)

**A.** Linha1 **B.** Quantidade **C.** Quantidade Total

Agora, você deseja adicionar quantidades especificadas na coluna Quantidade do Produto para todos os produtos e exibir a soma na célula Quantidade Total. Você pode fazer isso gravando uma regra Definir valor de na célula Quantidade total, como mostrado abaixo.

![exemplo-saída-função](assets/example-function-output.png)

Regra no editor visual

A regra é exibida da seguinte maneira no editor de código.

![exemplo-função-código-saída](assets/example-function-output-code.png)

Regra no editor de código

### Validação de um valor de campo usando expressão {#validating-a-field-value-using-expression}

No form ordem de compra explicado no exemplo anterior, você deseja impedir que o usuário faça pedidos de mais de uma quantidade de qualquer produto com preço superior a 10000. Para fazer isso, você pode escrever uma regra Validate como mostrado abaixo.

![exemplo-validar](assets/example-validate.png)

Regra no visual editor

A regra é exibida da seguinte maneira na editor de código.

![exemplo de código validado](assets/example-validate-code.png)

Regra no código editor
