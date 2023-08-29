---
title: Editor de regras de formulários adaptáveis
seo-title: Adaptive forms rule editor
description: O editor de regras de formulários adaptáveis permite adicionar comportamento dinâmico e criar lógica complexa em formulários sem codificação ou script.
seo-description: Adaptive forms rule editor lets you add dynamic behavior and build complex logic into forms without coding or scripting.
uuid: c1b3d6e4-6f36-4352-ab57-9850d718e47c
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1b905e66-dc05-4f14-8025-62a78feef12a
docset: aem65
feature: Adaptive Forms
exl-id: c611a1f8-9d94-47f3-bed3-59eef722bf98
source-git-commit: 0985e591df83c7f1604bac37af771e8a7a21e691
workflow-type: tm+mt
source-wordcount: '6983'
ht-degree: 0%

---

# Editor de regras de formulários adaptáveis{#adaptive-forms-rule-editor}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html) |
| AEM 6.5 | Este artigo |

## Visão geral {#overview}

O recurso do editor de regras no Adobe Experience Manager Forms permite que usuários e desenvolvedores de negócios de formulários gravem regras em objetos de formulário adaptáveis. Essas regras definem as ações a serem acionadas nos objetos de formulário com base nas condições predefinidas, entradas do usuário e ações do usuário no formulário. Isso ajuda a simplificar ainda mais a experiência de preenchimento de formulário, garantindo precisão e velocidade.

O editor de regras fornece uma interface de usuário intuitiva e simplificada para escrever regras. O editor de regras oferece um editor visual para todos os usuários. Além disso, somente para usuários avançados de formulários, o editor de regras fornece um editor de código para escrever regras e scripts. Algumas das principais ações que podem ser executadas em objetos de formulário adaptáveis usando regras do são:

* Mostrar ou ocultar um objeto
* Ativar ou desativar um objeto
* Definir um valor para um objeto
* Validar o valor de um objeto
* Executar funções para calcular o valor de um objeto
* Chame um serviço de modelo de dados de formulário e execute uma operação
* Definir a propriedade de um objeto

O Editor de regras substitui os recursos de script no AEM 6.1 Forms e em versões anteriores. No entanto, os scripts existentes são preservados no novo editor de regras. Para obter mais informações sobre como trabalhar com scripts existentes no editor de regras, consulte [Impacto do editor de regras nos scripts existentes](#impact-of-rule-editor-on-existing-scripts).

Os usuários adicionados aos grupo de recursos para formulários podem criar novos scripts e editar os existentes. Os usuários na grupo de formulários podem usar os scripts, mas não criar ou editar scripts.

## Noções básicas sobre um regra {#understanding-a-rule}

Uma regra é uma combinação de ações e condições. No editor de regras, as ações incluem atividades como ocultar, mostrar, habilitar, desabilitar ou calcular o valor de um objeto em um formulário. As condições são expressões booleanas que são avaliadas executando verificações e operações no estado, valor ou propriedade de um objeto de formulário. As ações são executadas com base no valor ( `True` ou `False`) retornado avaliando uma condição.

O editor de regras fornece um conjunto de tipos de regras predefinidos, como Quando, Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar, para ajudá-lo a escrever regras. Cada tipo de regra permite definir condições e ações em uma regra. O documento explica detalhadamente cada tipo de regra.

Uma regra normalmente segue uma das seguintes construções:

**Condição-Ação** Nesta construção, uma regra primeiro define uma condição seguida por uma ação para acionar. A construção é comparável à declaração if-then nas linguagens de programação.

No editor de regras, a variável **Quando** o tipo de regra impõe a construção condição-ação.

**Condição de ação** Nesta construção, uma regra primeiro define uma ação a ser acionada seguida por condições para avaliação. Outra variação dessa construção é ação-condição-ação alternativa, que também define uma ação alternativa a ser acionada se a condição retornar Falso.

Os tipos de regras Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar no editor de regras impõem a construção de regra de condição de ação. Por padrão, a ação alternativa para Mostrar é Ocultar, e para Habilitar é Desabilitar e vice-versa. Não é possível alterar a ação alternativa padrão.

>[!NOTE]
>
>Os tipos de regras disponíveis, incluindo condições e ações definidas no editor de regras, também dependem do tipo de objeto de formulário no qual você está criando uma regra. O editor de regras exibe somente tipos de regras válidos e opções para gravar instruções de condição e ação para um determinado tipo de objeto de formulário. Por exemplo, você não vê os tipos de regras Validar, Definir valor de, Ativar e Desativar para um objeto de painel.

Para obter mais informações sobre tipos de regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](#available-rule-types-in-rule-editor).

### Diretrizes para a escolha de uma construção de regra {#guidelines-for-choosing-a-rule-construct}

Embora seja possível obter a maioria dos casos de uso usando qualquer construção de regra, veja a seguir algumas diretrizes para escolher uma construção em vez de outra. Para obter mais informações sobre as regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](#available-rule-types-in-rule-editor).

* Uma regra prática comum ao criar uma regra é pensar nela no contexto do objeto no qual você está escrevendo uma regra. Considere que deseja ocultar ou mostrar o campo B com base no valor especificado por um usuário no campo A. Nesse caso, você está avaliando uma condição no campo A e, com base no valor retornado, aciona uma ação no campo B.

  Portanto, se estiver gravando uma regra no campo B (o objeto no qual você está avaliando uma condição), use a construção de condição-ação ou o tipo de regra When. Da mesma forma, use a construção action-condition ou o tipo de regra Mostrar ou Ocultar no campo A.

* Às vezes, você precisa executar várias ações com base em uma condição. Nesses casos, é recomendável usar a construção condição-ação. Nesta construção, você pode avaliar uma condição uma vez e especificar várias instruções de ação.

  Por exemplo, para ocultar os campos B, C e D com base na condição que verifica o valor especificado por um usuário no campo A, grave uma regra com construção de condição-ação ou Quando tipo de regra no campo A e especifique ações para controlar a visibilidade dos campos B, C e D. Caso contrário, você precisará de três regras separadas nos campos B, C e D, em que cada regra verifica a condição e mostra ou oculta o respectivo campo. Neste exemplo, é mais eficiente escrever o tipo de regra Quando em um objeto do que Mostrar ou Ocultar em três objetos.

* Para acionar uma ação com base em várias condições, é recomendável usar a construção action-condition. Por exemplo, para mostrar e ocultar o campo A avaliando as condições nos campos B, C e D, use Mostrar ou Ocultar tipo de regra no campo A.
* Use a construção de condição-ação ou condição de ação se a regra contiver uma ação para uma condição.
* Se uma regra verificar uma condição e executar uma ação imediatamente ao fornecer um valor em um campo ou ao sair de um campo, é recomendável gravar uma regra com construção de condição-ação ou o tipo de regra Quando no campo em que a condição é avaliada.
* A condição na regra Quando é avaliada quando um usuário altera o valor do objeto no qual a regra Quando é aplicada. No entanto, se você quiser que a ação seja acionada quando o valor for alterado no lado do servidor, como no caso de preenchimento prévio do valor, é recomendável gravar uma regra When que aciona a ação quando o campo é inicializado.
* Ao escrever regras para objetos de menus suspensos, botões de opção ou caixas de seleção, as opções ou os valores desses objetos de formulário no formulário são preenchidos previamente no editor de regras.

## Tipos de operadores e eventos disponíveis no editor de regras {#available-operator-types-and-events-in-rule-editor}

O editor de regras fornece os seguintes operadores lógicos e eventos com os quais você pode criar regras.

* **É Igual a**
* **Não é igual a**
* **Começa com**
* **Termina com**
* **Contém**
* **Está vazio**
* **Não está vazio**
* **Selecionou:** Retorna verdadeiro quando o usuário seleciona uma opção específica para uma caixa de seleção, botão de opção suspenso.
* **Inicializado (evento):** Retorna verdadeiro quando um objeto de formulário é renderizado no navegador.
* **Foi alterado (evento):** Retorna verdadeiro quando o usuário altera o valor inserido ou a opção selecionada para um objeto de formulário.

## Tipos de regras disponíveis no editor de regras {#available-rule-types-in-rule-editor}

O editor de regras fornece um conjunto de tipos de regras predefinidos que você pode usar para escrever regras. Vamos analisar cada tipo de regra detalhadamente. Para obter mais informações sobre como escrever regras no editor de regras, consulte [Regras de gravação](#write-rules).

### Quando {#whenruletype}

A variável **Quando** o tipo de regra segue a variável **condição-ação-ação alternativa** regra construir, ou às vezes, apenas a variável **condição-ação** construir. Nesse tipo de regra, primeiro especifique uma condição para avaliação seguida por uma ação para acionar se a condição for atendida ( `True`). Ao usar o tipo de regra Quando, é possível usar vários operadores E e OU para criar [expressões aninhadas](#nestedexpressions).

Usando o tipo de regra Quando, é possível avaliar uma condição em um objeto de formulário e executar ações em um ou mais objetos.

Em palavras simples, uma regra When típica é estruturada da seguinte maneira:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Ação 2 no objeto B;
E
Ação 3 no Objeto C;

_

Quando você tem um componente de vários valores, como botões de opção ou lista, ao criar um regra para esse componente, as opções são recuperadas automaticamente e disponibilizadas ao criador do regra. Não é necessário digitar os valores da opção novamente.

Por exemplo, um lista tem quatro opções: Vermelho, Azul, Verde e Amarelo. Ao criar a regra, as opções (botões de opção) são recuperadas e disponibilizadas automaticamente ao regra criador como a seguir:

![multivaluefcdisplaysoptions](assets/multivaluefcdisplaysoptions.png)

Ao escrever uma regra Quando, é possível acionar a ação Limpar valor de. Limpar valor da ação limpa o valor do objeto especificado. Ter o valor claro de como uma opção na instrução When permite criar condições complexas com vários campos.

![clearvalueof](assets/clearvalueof.png)

**Oculta** o objeto especificado.

**** Exibir Mostra o objeto especificado.

**Ativar** Habilita o objeto especificado.

**Desativar** Desabilita o objeto especificado.

**Chamar serviço** Invoca um serviço configurado em um modelo de dados de formulário. Quando você escolhe a operação Chamar Serviço, um campo é exibido. Ao tocar no campo, ele exibe todos os serviços configurados em todos os modelos de dados de formulário na instância do AEM. Ao escolher um serviço de modelo de dados de formulário, campos adicionais são exibidos onde você pode mapear objetos de formulário com parâmetros de entrada e saída para o serviço especificado. Consulte exemplo de regra para chamar serviços de modelo de dados de formulário.

Além do serviço de modelo de dados de formulário, você pode especificar um URL WSDL direto para chamar um serviço Web. No entanto, um serviço de modelo de dados de formulário tem muitos benefícios e a abordagem recomendada para chamar um serviço.

Para obter mais informações sobre como configurar serviços no modelo de dados de formulário, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

**Definir valor de** Calcula e define o valor do objeto especificado. Você pode definir o valor do objeto como uma string, o valor de outro objeto, o valor calculado usando expressão matemática ou função, o valor de uma propriedade de um objeto ou o valor de saída de um serviço de modelo de dados de formulário configurado. Quando você escolhe a opção de serviço da Web, ela exibe todos os serviços configurados em todos os modelos de dados de formulário na sua instância do AEM. Ao escolher um serviço de modelo de dados de formulário, campos adicionais são exibidos onde você pode mapear objetos de formulário com parâmetros de entrada e saída para o serviço especificado.

Para obter mais informações sobre como configurar serviços no modelo de dados de formulário, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

A variável **[!UICONTROL Definir propriedade]** o tipo de regra permite definir o valor de uma propriedade do objeto especificado com base em uma ação de condição. Você pode definir a propriedade como uma das seguintes opções:
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

Para definir uma regra com base em uma função personalizada, selecione **Saída da função** na lista suspensa e arraste e solte uma função personalizada do **Funções** guia. Se a ação de condição for atendida, o número de caixas de seleção definidas na função personalizada será adicionado ao formulário adaptável.

Para definir uma regra com base em um objeto de formulário, selecione **Objeto de formulário** na lista suspensa e arraste e solte um objeto de formulário da **Objetos de formulário** guia. Se a ação de condição for atendida, o número de caixas de seleção definidas no objeto de formulário será adicionado ao formulário adaptável.

Uma regra Definir propriedade com base em uma propriedade de objeto permite adicionar o número de caixas de seleção em um formulário adaptável com base em outra propriedade de objeto incluída no formulário adaptável.

A figura a seguir mostra um exemplo de adição dinâmica de caixas de seleção com base no número de listas suspensas no formulário adaptável:

![Propriedade do objeto](assets/object_property_set_property_new.png)

**Limpar Valor de** Limpa o valor do objeto especificado.

**Definir Foco** Define o foco para o objeto especificado.

**Salvar formulário** Salva o formulário.

**Enviar Forms** Envia o formulário.

**Redefinir formulário** Redefine o formulário.

**Validar Formulário** Valida o formulário.

**Adicionar instância** Adiciona uma ocorrência da linha de tabela ou painel repetível especificada.

**Remover Instância** Remove uma ocorrência da linha de tabela ou painel repetível especificada.

**Navegue até** Navega até outras Comunicações interativas, formulários adaptáveis, outros ativos, como imagens ou fragmentos de documentos, ou um URL externo. Para obter mais informações, consulte [Botão Adicionar à comunicação interativa](../../forms/using/create-interactive-communication.md#addbuttontothewebchannel).

### Definir valor de {#set-value-of}

A variável **[!UICONTROL Definir valor de]** o tipo de regra permite definir o valor de um objeto de formulário dependendo se a condição especificada é atendida ou não. O valor pode ser definido como um valor de outro objeto, uma string literal, um valor derivado de uma expressão matemática ou de uma função, um valor de uma propriedade de outro objeto ou a saída de um serviço de modelo de dados de formulário. Da mesma forma, você pode verificar uma condição em um componente, string, propriedade ou valores derivados de uma função ou expressão matemática.

Observe que o tipo de regra Definir valor de não está disponível para todos os objetos de formulário, como painéis e botões da barra de ferramentas. Uma regra padrão Definir valor de tem a seguinte estrutura:



Defina o valor do Objeto A como:

(cadeia de caracteres ABC) OR (propriedade do objeto X do objeto C) OR (valor de uma função) OR (valor de uma expressão matemática) OR (valor de saída de um serviço de modelo de dados ou serviço Web);

Quando (opcional):

(Condição 1 E Condição 2 E Condição 3) é VERDADEIRA;



O exemplo a seguir usa o valor em `dependentid` campo como entrada e define o `Relation` valor do campo para a saída do `Relation` argumento do serviço de modelo de dados de `getDependent` formulário.

![set-value-Web-service](assets/set-value-web-service.png)

Exemplo de Definir Valor regra usando o serviço de modelo de dados de formulário

>[!NOTE]
>
>Além disso, você pode usar Definir Valor de regra para preencher todos os valores em um componente lista suspenso da saída de um serviço de modelo de dados de formulário ou de um serviço da Web. No entanto, certifique-se de que o argumento de saída escolhido é de um tipo de matriz. Todos os valores retornados em uma matriz ficam disponíveis na lista suspensa especificada.

### Mostrar {#show}

Usar o **Mostrar** tipo de regra, é possível escrever uma regra para mostrar ou ocultar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Mostrar também aciona a ação Ocultar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de exibição está estruturada da seguinte maneira:



`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`



### Ocultar {#hide}

Semelhante ao tipo de regra Mostrar, é possível usar a variável **Ocultar** tipo de regra para mostrar ou ocultar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Ocultar também aciona a ação Mostrar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de Ocultar está estruturada da seguinte maneira:



`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`



### Ativar {#enable}

A variável **Ativar** o tipo de regra permite ativar ou desativar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Ativar também aciona a ação Desativar caso a condição não seja atendida ou retornada `False`.

Uma regra Enable típica é estruturada da seguinte maneira:



`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`



### Desativar {#disable}

Semelhante ao tipo de regra Ativar, a variável **Desativar** o tipo de regra permite ativar ou desativar um objeto de formulário com base no fato de uma condição ser atendida ou não. O tipo de regra Desativar também aciona a ação Ativar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de Desativação está estruturada da seguinte maneira:



`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### Validar {#validate}

A variável **Validar** o tipo de regra valida o valor em um campo usando uma expressão. Por exemplo, você pode escrever uma expressão para verificar se a caixa de texto para especificar o nome não contém caracteres especiais ou números.

Uma regra Validate típica é estruturada da seguinte maneira:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se o valor especificado não estiver em conformidade com a regra Validar, você poderá exibir uma mensagem de validação para o usuário. Você pode especificar a mensagem nas **[!UICONTROL Mensagem de validação do script]** nas propriedades do componente na barra lateral.

![script-validation](assets/script-validation.png)

### Definir Opções De {#setoptionsof}

A variável **Definir Opções De** o tipo de regra permite definir regras para adicionar caixas de seleção dinamicamente ao formulário adaptável. Você pode usar um modelo de dados de formulário ou uma função personalizada para definir a regra.

Para definir uma regra com base em uma função personalizada, selecione **Saída da função** na lista suspensa e arraste e solte uma função personalizada do **Funções** guia. O número de caixas de seleção definidas na função personalizada é adicionado ao formulário adaptável.

![Funções personalizadas](assets/custom_functions_set_options_new.png)

Para criar uma função personalizada, consulte [funções personalizadas no editor de regras](#custom-functions).

Para definir uma regra baseada em um modelo de dados de formulário:

1. Selecionar **Saída do serviço** na lista suspensa.
1. Selecione o objeto de modelo de dados.
1. Selecione uma propriedade de objeto de modelo de dados na **Valor de Exibição** lista suspensa. O número de caixas de seleção no formulário adaptável é derivado do número de instâncias definidas para essa propriedade no banco de dados.
1. Selecione uma propriedade de objeto de modelo de dados na **Salvar valor** lista suspensa.

![Opções de definição de FDM](assets/fdm_set_options_new.png)

## Noções básicas sobre a interface do usuário do editor de regras {#understanding-the-rule-editor-user-interface}

O Editor de regras fornece uma interface de usuário abrangente, mas simples, para gravar e gerenciar regras. É possível iniciar a interface do usuário do editor de regras a partir de um formulário adaptável no modo de criação.

Para iniciar a interface do usuário do editor de regras:

1. Abra um formulário adaptável no modo de criação.
1. Toque no objeto de formulário para o qual deseja escrever uma regra e, na Barra de ferramentas de componentes, toque em ![edit-rules](assets/edit-rules.png). A interface do usuário do editor de regras é exibida.

   ![create-rules](assets/create-rules.png)

   Todas as regras existentes nos objetos de formulário selecionados são listadas nessa exibição. Para obter informações sobre como gerenciar regras existentes, consulte [Gerenciar regras](#manage-rules).

1. Toque **[!UICONTROL Criar]** para escrever uma nova regra. O editor visual da interface do usuário do editor de regras é aberto por padrão quando você inicia o editor de regras pela primeira vez.

   ![Interface do Editor de regras](assets/rule-editor-ui.png)

Vamos analisar cada componente da interface do editor de regras em detalhes.

### A. Exibição de componente-regra {#a-component-rule-display}

Exibe o título do objeto de formulário adaptável pelo qual você iniciou o editor de regras e o tipo de regra selecionado no momento. No exemplo acima, o editor de regras é iniciado a partir de um objeto de formulário adaptável chamado Salário, e o tipo de regra selecionado é Quando.

### B. Funções e objetos de formulário {#b-form-objects-and-functions-br}

O painel à esquerda na interface do editor de regras inclui duas guias: **[!UICONTROL Objetos do Forms]** e **[!UICONTROL Funções]**.

A guia Objetos de formulário mostra uma exibição hierárquica de todos os objetos contidos no formulário adaptável. Ele exibe o título e o tipo dos objetos. Ao escrever uma regra, você pode arrastar e soltar objetos de formulário no editor de regras. Ao criar ou editar uma regra ao arrastar e soltar um objeto ou função em um espaço reservado, o espaço reservado automaticamente assume o tipo de valor apropriado.

Os objetos de formulário que têm uma ou mais regras válidas aplicadas são marcados com um ponto verde. Se alguma das regras aplicadas a um objeto de formulário for inválida, o objeto de formulário será marcado com um ponto amarelo.

A guia Funções inclui um conjunto de funções incorporadas, como Soma de, Mín de, Máx de, Média de, Número de e Validar formulário. Você pode usar essas funções para calcular valores em painéis e linhas de tabela repetíveis e usá-los em declarações de ação e condição ao escrever regras. No entanto, você pode criar [funções personalizadas](#custom-functions) também.

![A guia Funções](assets/functions.png)

>[!NOTE]
>
>Você pode executar a pesquisa de texto em nomes de objetos e funções e títulos nas guias Objetos e Funções do Forms.

Na árvore esquerda dos objetos de formulário, toque nos objetos de formulário para exibir as regras aplicadas a cada um deles. Você não só pode navegar pelas regras dos vários objetos de formulário, como também pode copiar e colar regras entre os objetos de formulário. Para obter mais informações, consulte [Copiar e colar regras](#copy-paste-rules).

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
1. escolher **[!UICONTROL Editor visual]** ou **[!UICONTROL Editor de código]** do **[!UICONTROL Modo padrão do Editor de regras]** menu suspenso

1. Clique em **[!UICONTROL Salvar]**.

### F. Botões Concluído e Cancelar {#f-done-and-cancel-buttons}

A variável **[!UICONTROL Concluído]** é usado para salvar uma regra. Você pode salvar uma regra incompleta. No entanto, incompletos são inválidos e não são executados. As regras salvas em um objeto de formulário são listadas na próxima vez que você iniciar o editor de regras a partir do mesmo objeto de formulário. Você pode gerenciar as regras existentes nessa visualização. Para obter mais informações, consulte [Gerenciar regras](#manage-rules).

A variável **[!UICONTROL Cancelar]** O botão descarta todas as alterações feitas em uma regra e fecha o editor de regras.

## Regras de gravação {#write-rules}

É possível escrever regras usando o editor visual de regras ou o editor de códigos. Quando você inicia o editor de regras pela primeira vez, ele é aberto no modo do editor visual. Você pode alternar para o modo do editor de código e escrever regras. No entanto, observe que, se você escrever ou modificar uma regra no editor de códigos, não poderá alternar para o editor visual dessa regra, a menos que o editor de códigos seja limpo. Na próxima vez que você iniciar o editor de regras, ele será aberto no modo usado por último para criar a regra.

Primeiro, vamos analisar como escrever regras usando o editor visual.

### Uso do editor visual {#using-visual-editor}

Vamos entender como criar uma regra no editor visual usando o seguinte formulário de exemplo.

![create-rule-example](assets/create-rule-example.png)

A seção Requisitos de Empréstimo no formulário de solicitação de empréstimo de exemplo exige que os candidatos especifiquem seu estado civil, salário e, se forem casados, o salário de seus cônjuges. Com base nas entradas do usuário, a regra calcula o valor de qualificação de empréstimo e é exibida no campo Elegibilidade do empréstimo. Aplique as seguintes regras para implementar o cenário:

* O campo Salário do Cônjuge é exibido somente quando o Estado Civil é Casado.
* O valor de qualificação de empréstimo é de 50% do salário total.

Execute as seguintes etapas para escrever regras:

1. Primeiro, escreva a regra para controlar a visibilidade do campo Salário do Cônjuge com base na opção que o usuário seleciona para o botão de opção Estado Civil.

   Abra o formulário de solicitação de empréstimo no modo de criação. Toque no **Estado civil** componente e toque em ![edit-rules](assets/edit-rules.png). Em seguida, toque em **[!UICONTROL Criar]** para iniciar o editor de regras.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Ao iniciar o editor de regras, a regra Quando é selecionada por padrão. Além disso, o objeto de formulário (nesse caso, Estado civil) de onde você iniciou o editor de regras é especificado na instrução When.

   Embora não seja possível alterar ou modificar o objeto selecionado, você poderá usar o menu suspenso de regras, como mostrado abaixo, para selecionar outro tipo de regra. Se quiser criar uma regra em outro objeto, toque em Cancelar para sair do editor de regras e iniciá-lo novamente a partir do objeto de formulário desejado.

1. Toque **[!UICONTROL Selecionar Estado]** e selecione **[!UICONTROL é igual a]**. A variável **[!UICONTROL Insira uma string]** é exibido.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   No botão de opção Estado Civil, **Casado** e **Solteiro** opções são atribuídas **0** e **1** valores, respectivamente. Você pode verificar os valores atribuídos na guia Título da caixa de diálogo Editar botão de opção, conforme mostrado abaixo.

   ![Valores do botão de opção do editor de regras](assets/radio-button-values.png)

1. No **Insira uma string** na regra, especifique **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   Você definiu a condição como `When Marital Status is equal to Married`. Em seguida, defina a ação a ser executada se essa condição for True.

1. Na instrução Then, selecione **[!UICONTROL Mostrar]** do **[!UICONTROL Selecionar ação]** menu suspenso.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Arraste e solte a **Salário do Cônjuge** da guia Objetos de formulário no **Soltar objeto ou selecionar aqui** campo. Como alternativa, toque no **Soltar objeto ou selecionar aqui** e selecione o **Salário do Cônjuge** no menu pop-up, que lista todos os objetos de formulário no formulário.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   A regra é exibida da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

   Toque **Concluído** para salvar a regra.

1. Repita as etapas de 1 a 5 para definir outra regra para ocultar o campo Salário do Cônjuge se o estado civil for Simples. A regra é exibida da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >Como alternativa, você pode escrever uma regra Mostrar no campo Salário do Cônjuge, em vez de duas regras Quando no campo Estado Civil, para implementar o mesmo comportamento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Em seguida, escreva uma regra para calcular o valor de qualificação de empréstimo, que é 50% do salário total, e exiba-o no campo Elegibilidade do empréstimo. Para isso, crie **Definir valor de** regras no campo Elegibilidade do empréstimo.

   No modo de criação, toque no **[!UICONTROL Elegibilidade do empréstimo]** e toque em ![edit-rules](assets/edit-rules.png). Em seguida, toque em **[!UICONTROL Criar]** para iniciar o editor de regras.

1. Selecionar **[!UICONTROL Definir Valor De]** regra no menu suspenso de regras.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Toque **[!UICONTROL Selecionar opção]** e selecione **[!UICONTROL Expressão matemática]**. Um campo para escrever expressão matemática é aberto.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. No campo de expressão:

   * Selecione ou arraste e solte na guia Objeto do Forms o **Salário** no primeiro **Soltar objeto ou selecionar aqui** campo.

   * Selecionar **Plus** do **Selecionar operador** campo.

   * Selecione ou arraste e solte na guia Objeto do Forms o **Salário do Cônjuge** no outro **Soltar objeto ou selecionar aqui** campo.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Em seguida, toque na área realçada ao redor do campo de expressão e toque em **Estender expressão**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   No campo extended expression, selecione **dividido por** do **Selecionar operador** campo e **Número** do **Selecionar opção** campo. Em seguida, especifique **2** no campo de número.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >Você pode criar expressões complexas usando componentes, funções, expressões matemáticas e valores de propriedade no campo Selecionar opção.

   Em seguida, crie uma condição, que quando retorna True, a expressão é executada.

1. Toque **Adicionar Condição** para adicionar uma instrução When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Na instrução When:

   * Selecione ou arraste e solte na guia Objeto do Forms o **Estado civil** no primeiro **Soltar objeto ou selecionar aqui** campo.

   * Selecionar i **s igual a** do **Selecionar operador** campo.

   * Selecionar string no outro **Soltar objeto ou selecionar aqui** campo e especificar **Casado** no **Insira uma string** campo.

   A regra finalmente aparece da seguinte maneira no editor de regras.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

   Toque **Concluído** para salvar a regra.

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

O JavaScript do editor de código é a linguagem de expressão de formulários adaptáveis. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de determinados tipos. Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

Para obter mais informações sobre diretrizes para escrever regras no editor de código, consulte [Expressões de formulário adaptável](/help/forms/using/adaptive-form-expressions.md).

Ao escrever código JavaScript no editor de regras, as seguintes dicas visuais o ajudam com a estrutura e a sintaxe:

* Destaques da sintaxe
* Recuo Automático
* Dicas e sugestões para objetos de formulário, funções e suas propriedades
* Preenchimento automático de nomes de componentes de formulário e funções JavaScript comuns

![javascriptruleeditor](assets/javascriptruleeditor.png)

#### Funções personalizadas no editor de regras {#custom-functions}

Além das funções prontas para uso como *Soma de* que estão listados em Saída de funções, você pode gravar funções personalizadas que você precisa com frequência. Certifique-se de que a função gravada esteja acompanhada pelo `jsdoc` acima dele.

Acompanhando `jsdoc` é obrigatório:

* Se desejar configuração e descrição personalizadas.
* Como há várias maneiras de declarar uma função no `JavaScript,` Os comentários do e do permitem rastrear as funções.

Para obter mais informações, consulte [usejsdoc.org](https://jsdoc.app/).

Compatível `jsdoc` tags:

* **Privado**
Sintaxe: `@private`
Uma função privada não está incluída como uma função personalizada.

* **Nome**
Sintaxe: `@name funcName <Function Name>`
Alternativamente `,` você pode usar: `@function funcName <Function Name>` **ou** `@func` `funcName <Function Name>`.
  `funcName` é o nome da função (sem espaços).
  `<Function Name>` é o nome de exibição da função.

* **membro**
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

* **Tipo de retorno**
Sintaxe: `@return {type}`
Como alternativa, você pode usar `@returns {type}`.
Adiciona informações sobre a função, como seu objetivo.
{type} representa o tipo de retorno da função. Os tipos de retorno permitidos são:

   1. string
   1. número
   1. booleano

  Todos os outros tipos de retorno são categorizados em um dos itens acima. Nenhum não é compatível. Selecione um dos tipos acima. Os tipos de retorno não diferenciam maiúsculas de minúsculas.

* **Este**
Sintaxe: `@this currentComponent`

  Use @this para se referir ao componente de Formulário adaptável no qual a regra é gravada.

  O exemplo a seguir é baseado no valor do campo. No exemplo a seguir, a regra oculta um campo no formulário. A variável `this` parte de `this.value` refere-se ao componente de Formulário adaptável subjacente, no qual a regra é gravada.

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

**Adição de uma função personalizada**

Por exemplo, você deseja adicionar uma função personalizada que calcula a área de um quadrado. O comprimento do lado é a entrada do usuário na função personalizada, que é aceita usando uma caixa numérica no formulário. A saída calculada é exibida em outra caixa numérica no formulário. Para adicionar uma função personalizada, primeiro crie uma biblioteca do cliente e, em seguida, adicione-a ao repositório CRX.

Execute as etapas a seguir para criar uma biblioteca do cliente e adicioná-la ao repositório CRX.

1. Crie uma biblioteca do cliente. Para obter mais informações, consulte [Uso de bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md).
1. No CRXDE, adicione uma propriedade `categories`com valor de tipo de string como `customfunction` para o `clientlib` pasta.

   >[!NOTE]
   >
   >`customfunction`é uma categoria de exemplo. Você pode escolher qualquer nome para a categoria que criar na `clientlib`pasta.

Depois de ter adicionado a biblioteca do cliente ao repositório CRX, use-a no formulário adaptável. Ela permite usar sua função personalizada como uma regra em seu formulário. Execute as seguintes etapas para adicionar a biblioteca do cliente no formulário adaptável.

1. Abra o formulário no modo de edição.
Para abrir um formulário no modo de edição, selecione um formulário e toque em **Abertura**.
1. No modo de edição, selecione um componente e toque em ![nível de campo](assets/field-level.png) > **Contêiner de formulário adaptável** e toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, em Nome da biblioteca do cliente, adicione a biblioteca do cliente. ( `customfunction` no exemplo.)

   ![Adição da biblioteca de cliente de função personalizada](assets/clientlib.png)

1. Selecione a caixa numérica de entrada e toque em ![edit-rules](assets/edit-rules.png) para abrir o editor de regras.
1. Toque **Criar regra**. Usando as opções mostradas abaixo, crie uma regra para salvar o valor quadrado da entrada no campo Output do formulário.
   [![Utilização de funções personalizadas para criar uma regra](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)Toque **Concluído**. Sua função personalizada é adicionada.

#### Tipos suportados de declaração de função {#function-declaration-supported-types}

**Declaração de função**

```javascript
function area(len) {
    return len*len;
}
```

Esta função é incluída sem `jsdoc` comentários.

**Expressão de função**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Expressão e instrução de função**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Declaração de função como variável**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitação: a função personalizada escolhe somente a primeira declaração de função da lista de variáveis, se estiver junto. Você pode usar a expressão de função para cada função declarada.

**Declaração de função como objeto**

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
>Certifique-se de usar `jsdoc` para cada função personalizada. Embora `jsdoc`os comentários são incentivados, inclua um vazio `jsdoc`comentário para marcar sua função como função personalizada. Ela permite o tratamento padrão da função personalizada.

## Gerenciar regras {#manage-rules}

Todas as regras existentes em um objeto de formulário são listadas ao tocar no objeto e tocar ![edit-rules1](assets/edit-rules1.png). É possível exibir o título e uma pré-visualização do resumo da regra. Além disso, a interface do permite expandir e exibir o resumo completo da regra, alterar a ordem das regras, editar regras e excluir regras.

![list-rules](assets/list-rules.png)

Você pode executar as seguintes ações nas regras:

* **Expandir/Recolher**: A coluna Conteúdo na lista de regras exibe o conteúdo da regra. Se todo o conteúdo da regra não estiver visível na exibição padrão, toque em ![expand-rule-content](assets/expand-rule-content.png) para expandi-la.

* **Reordenar**: qualquer nova regra criada é empilhada na parte inferior da lista de regras. As regras são executadas de cima para baixo. A regra na parte superior é executada primeiro, seguida por outras regras do mesmo tipo. Por exemplo, se você tiver as regras When, Show, Enable e When na primeira, segunda, terceira e quarta posições acima, respectivamente, a regra When na parte superior será executada primeiro, seguida pela regra When na quarta posição. Em seguida, as regras Show e Enable serão executadas.
É possível alterar a ordem de uma regra tocando ![sort-rules](assets/sort-rules.png) contra ele ou arraste-o e solte-o na ordem desejada na lista.

* **Editar**: para editar uma regra, marque a caixa de seleção ao lado do título da regra. São exibidas opções adicionais para editar e excluir a regra. Toque **Editar** para abrir a regra selecionada no editor de regras no modo visual ou editor de códigos, dependendo do modo usado para criar a regra.

* **Excluir**: para excluir uma regra, selecione-a e toque em **Excluir**.

* **Ativar/desativar**: talvez seja necessário suspender temporariamente o uso de uma regra. Você pode selecionar uma ou mais regras e tocar em Desativar na barra de ferramentas Ações para desativá-las. Se uma regra estiver desativada, ela não será executada no tempo de execução. Para habilitar uma regra que esteja desabilitada, selecione-a e toque em Habilitar na barra de ferramentas de ações. A coluna de status da regra exibe se a regra está ativada ou desativada.

![disablerule](assets/disablerule.png)

## Copiar e colar regras {#copy-paste-rules}

É possível copiar e colar uma regra de um campo para outros campos semelhantes para economizar tempo.

Para copiar e colar regras, faça o seguinte:

1. Toque no objeto de formulário do qual deseja copiar uma regra e, na barra de ferramentas do componente, toque em ![editrule](assets/editrule.png). A interface do usuário do editor de regras é exibida com o objeto de formulário selecionado e as regras existentes são exibidas.

   ![copyrule](assets/copyrule.png)

   Para obter informações sobre como gerenciar regras existentes, consulte [Gerenciar regras](#manage-rules).

1. Marque a caixa de seleção ao lado do título da regra. São exibidas opções adicionais para gerenciar a regra. Toque em **Copiar**.

   ![copyrule2](assets/copyrule2.png)

1. Selecione outro objeto de formulário no qual deseja colar a regra e toque **Colar**. Além disso, você pode editar a regra para alterá-la.

   >[!NOTE]
   >
   >Você só poderá colar uma regra em outro objeto de formulário se esse objeto der suporte ao evento da regra copiada. Por exemplo, um botão oferece suporte ao evento click. É possível colar uma regra com um evento de clique em um botão, mas não em uma caixa de seleção.

1. Toque **Concluído** para salvar a regra.

## Expressões aninhadas {#nestedexpressions}

O editor de regras permite usar vários operadores AND e OR para criar regras aninhadas. Você pode misturar vários operadores AND e OR em regras.

Veja a seguir um exemplo de uma regra aninhada que exibe uma mensagem ao usuário sobre a elegibilidade para a custódia de uma criança quando as condições necessárias são atendidas.

![expressão complexa](assets/complexexpression.png)

Também é possível arrastar e soltar condições em uma regra para editá-la. Toque e passe o mouse sobre a alça ( ![identificador](assets/handle.png)) antes de uma condição. Depois que o ponteiro se transformar no símbolo da mão, como mostrado abaixo, arraste e solte a condição em qualquer lugar dentro da regra. A estrutura da regra muda.

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

![revisão adicional solicitada](assets/additionalproofrequested.png)

## Impacto do editor de regras nos scripts existentes {#impact-of-rule-editor-on-existing-scripts}

Nas versões do AEM Forms anteriores ao AEM 6.1 Forms feature pack 1, os autores e desenvolvedores de formulário costumavam escrever expressões na guia Scripts da caixa de diálogo Editar componente para adicionar comportamento dinâmico a formulários adaptáveis. A guia Scripts agora é substituída pelo editor de regras.

Todos os scripts ou expressões que você deve ter escrito na guia Scripts estão disponíveis no editor de regras. Embora não seja possível visualizá-los ou editá-los no editor visual, se você fizer parte do grupo de formulários-usuários avançados, será possível editar scripts no editor de código.

## Exemplo de regras {#example}

### Chamar serviço de modelo de dados de formulário {#invoke}

Considerar um serviço Web `GetInterestRates` que usa o valor do empréstimo, a estabilidade financeira e a pontuação de crédito do candidato como entrada e retorna um plano de empréstimo incluindo o valor da EMI e a taxa de juros. Crie um modelo de dados de formulário usando o serviço Web como uma fonte de dados. Você adiciona objetos de modelo de dados e um `get` para o modelo de formulário. O serviço aparece na guia Serviços do modelo de dados de formulário. Em seguida, crie um formulário adaptável que inclua campos de objetos de modelo de dados para capturar as entradas do usuário para valor do empréstimo, estabilidade e pontuação de crédito. Adicione um botão que aciona o serviço Web para buscar detalhes do plano. A saída é preenchida nos campos apropriados.

A regra a seguir mostra como você configurará a ação Chamar serviço para realizar o cenário de exemplo.

![example-invoke-services](assets/example-invoke-services.png)

Invocar o serviço de modelo de dados de formulário usando a regra de formulário adaptável

>[!NOTE]
>
>Se a entrada for do tipo matriz, os campos compatíveis com matrizes estarão visíveis na seção suspensa Saída.

### Acionamento de várias ações usando a regra Quando {#triggering-multiple-actions-using-the-when-rule}

Em um formulário de solicitação de empréstimo, você deseja registrar se o candidato ao empréstimo é um cliente existente ou não. Com base nas informações fornecidas pelo usuário, o campo ID do cliente deve mostrar ou ocultar. Além disso, é possível definir o foco no campo ID do cliente se o usuário for um cliente existente. O formulário de pedido de empréstimo tem os seguintes componentes:

* Um botão de opção, **Você já é cliente do Geometrixx?**, que fornece as opções Sim e Não. O valor de Sim é **0** e Não é **1**.

* Um campo de texto, **ID de cliente do Geometrixx**, para especificar a ID do cliente.

Quando você escreve uma regra Quando no botão de opção para implementar esse comportamento, a regra é exibida da seguinte maneira no editor visual de regras.  ![when-rule-example](assets/when-rule-example.png)

Regra no editor visual

Na regra de exemplo, a instrução na seção When é a condição, que quando retorna True, executa as ações especificadas na seção Then.

A regra é exibida da seguinte maneira no editor de código.

![when-rule-example-code](assets/when-rule-example-code.png)

Regra no editor de código

### Uso de uma saída de função em uma regra {#using-a-function-output-in-a-rule}

Em um formulário de ordem de compra, você tem a tabela a seguir, na qual os usuários preencherão seus pedidos. Nesta tabela:

* A primeira linha pode ser repetida, para que os usuários possam solicitar vários produtos e especificar quantidades diferentes. Seu nome de elemento é `Row1`.
* O título da célula na coluna Quantidade do Produto da linha repetível é Quantidade. O nome do elemento para esta célula é `productquantity`.
* A segunda linha da tabela não pode ser repetida e o título da célula na coluna Quantidade do Produto nesta linha é Quantidade Total.

![exemplo-tabela-função](assets/example-function-table.png)

**A.** Linha1 **B.** Quantidade **C** Quantidade Total

Agora, você deseja adicionar quantidades especificadas na coluna Quantidade do Produto para todos os produtos e exibir a soma na célula Quantidade Total. Você pode fazer isso gravando uma regra Definir valor de na célula Quantidade total, como mostrado abaixo.

![exemplo-função-saída](assets/example-function-output.png)

Regra no editor visual

A regra é exibida da seguinte maneira no editor de código.

![example-function-output-code](assets/example-function-output-code.png)

Regra no editor de código

### Validação de um valor de campo usando expressão {#validating-a-field-value-using-expression}

No form ordem de compra explicado no exemplo anterior, você deseja impedir que o usuário faça pedidos de mais de uma quantidade de qualquer produto com preço superior a 10000. Para fazer isso, você pode escrever uma regra Validate como mostrado abaixo.

![example-validate](assets/example-validate.png)

Regra no editor visual

A regra é exibida da seguinte maneira no editor de código.

![example-validate-code](assets/example-validate-code.png)

Regra no editor de código
