---
title: Criação de formulários adaptáveis acessíveis
seo-title: Creating accessible adaptive forms
description: O AEM Forms fornece ferramentas e para criar formulários adaptáveis acessíveis, além de ajudar a estar em conformidade com os padrões de acessibilidade.
seo-description: AEM Forms provides you tools and to create accessible adaptive forms and helps comply with accessibility standards.
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
feature: Adaptive Forms
exl-id: e755159f-374f-42b8-b28b-e8864df44f9d
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 1%

---

# Criação de formulários adaptáveis acessíveis{#creating-accessible-adaptive-forms}

## Introdução {#introduction}

Um formulário acessível é um formulário que todos podem usar, incluindo usuários com necessidades especiais. O Adaptive Forms inclui vários recursos e funcionalidades que melhoram a utilização para usuários com diferentes capacidades. Criar a acessibilidade em formulários adaptáveis não só permite o maior público-alvo possível para o conteúdo, como também é um requisito ao fornecer documentos em regiões onde a conformidade com os padrões de acessibilidade é obrigatória. Os desenvolvedores de formulários de ajuda da AEM Forms estão em conformidade com os padrões de acessibilidade.

Ao criar um formulário adaptável, o autor deve considerar os seguintes pontos para criar um formulário adaptável acessível:

* Verifique o formulário com a ferramenta de teste de acessibilidade ANDI (Accessible Name and Description Inspetor)
* Fornecer rótulos adequados para controles de formulário
* Fornecer equivalentes de texto para imagens
* Fornecer contraste de cor suficiente
* Verifique se os controles de formulário são acessíveis ao teclado

## Pré-requisitos

Você precisa de uma ferramenta de acessibilidade, como **Inspetor de Nome e Descrição Acessível (ANDI)** e um **Tema de formulário adaptável desenvolvido para corrigir problemas relacionados à acessibilidade** para criar um formulário adaptável acessível.

### Baixe e instale a ferramenta de teste de acessibilidade

A ferramenta ANDI (Accessible Name and Description Inspetor) ajuda a identificar e corrigir problemas relacionados à conformidade de acessibilidade no conteúdo da Web. É a ferramenta recomendada sob as diretrizes do Trusted Tester v5 do Department of Homeland Security. Ele é desenvolvido pelo departamento &#x200B; Administração de Segurança Social dos Estados Unidos para verificar a conformidade da Seção 508 com o conteúdo da Web. A ferramenta:

* Ajuda a detectar problemas de acessibilidade &#x200B; em uma página da Web
* Fornece sugestões para melhorar a acessibilidade &#x200B;
* Detecta problemas de acessibilidade e contraste de cores do teclado
* Identifica claramente o conteúdo do leitor de tela em conformidade com os padrões

A ANDI funciona com todos os principais navegadores da Internet. Consulte [Documentação da ANDI](https://www.ssa.gov/accessibility/andi/help/install.html) para obter instruções detalhadas sobre como configurar e usar a ferramenta.

### Baixe e instale o tema acessível no Ultramarine

O tema do Ultramarine-Accessible é um tema de referência. Ajuda a demonstrar como corrigir o contraste de cores e outros problemas relacionados à acessibilidade em um formulário adaptável. O Adobe recomenda criar um tema personalizado para o ambiente de produção com base nos estilos aprovados por sua organização. Execute as seguintes etapas para fazer upload do tema para sua instância do AEM:

1. Baixe o pacote de temas.
1. Navegar para **[!UICONTROL Experience Manager]** > **[!UICONTROL Navegação]** ![Navegação](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]** na sua instância de AEM.
1. Toque **[!UICONTROL Criar]** > **[!UICONTROL Upload de arquivo]**. Selecione e carregue o arquivo x Ultramarine-Accessible-Theme.zip. Ele faz upload do tema para sua instância do AEM.

## Tornar um formulário adaptável acessível

Você deve se concentrar em quatro aspectos principais: navegação pelo teclado, contraste de cores, texto alternativo significativo para imagens e rótulos apropriados para controles de formulários para tornar um formulário adaptável acessível. Execute as seguintes etapas para tornar os formulários adaptáveis existentes acessíveis:

### 1. Aplique um tema acessível e execute correções adicionais

Aplique o tema acessível pelo Ultramarine ao formulário adaptável existente. Para aplicar o tema:

1. Abra o formulário adaptável para edição.
1. Selecione um componente e toque no ícone principal. No menu de contexto, toque em **[!UICONTROL Contêiner de formulário adaptável]** e toque no ícone configurar .
1. Selecione o tema acessível pelo ultramarine no navegador de propriedades e toque em **[!UICONTROL Salvar]** ícone .
1. Atualize a janela do navegador. O tema é aplicado à forma adaptativa.

Depois de aplicar um tema acessível, execute as correções adicionais listadas abaixo. As correções além das correções de acessibilidade abordadas no tema acessível:

1. Adicione um texto alternativo significativo para a imagem do logotipo no formulário adaptável.

   Forneça um texto alternativo significativo para imagens nos componentes de cabeçalho e rodapé do modelo de formulário adaptável. Ao corrigir o modelo e usá-lo para criar um formulário adaptável, os formulários adaptáveis herdam todas as correções relacionadas à acessibilidade aplicadas ao cabeçalho e rodapé do modelo.  Para um formulário adaptável existente, faça alterações no nível do formulário adaptável. As alterações feitas em um modelo de formulário adaptável não fluem automaticamente para um formulário adaptável existente.

1. Adicione um componente de cabeçalho contendo o nome do formulário ao formulário adaptável. Se o design de formulário especificar um nome de empresa, adicione também um componente de cabeçalho separado para o nome da empresa.

   A maioria das ferramentas de acessibilidade informa os usuários sobre a hierarquia do conteúdo para ajudá-los a entender a estrutura da página da Web. Defina níveis de cabeçalho diferentes para o texto do nome da organização e do nome do formulário no formulário adaptável para fornecer uma estrutura hierárquica para esse texto. Além disso, use um componente de Texto antes de cada painel e seção com um nível de cabeçalho apropriado para criar uma hierarquia.

   ![Como aplicar um estilo de cabeçalho](assets/apply-style.gif)

1. Altere a cor de fundo do rodapé para usar o contraste apropriado de acordo com os padrões de acessibilidade para melhorar a visibilidade e a legibilidade do texto. Você pode usar a ANDI para encontrar problemas de contraste de cores em seu formulário. Além disso, não use fonte muito pequena. Fontes pequenas são difíceis de ler.

1. Substitua os componentes switch e escolha de imagem em seu formulário adaptável existente pelo componente de escolha (rádio).

1. Substitua o componente passo numérico no formulário adaptável existente pelo componente caixa numérica.

1. Substitua o campo de entrada de data pelo campo do seletor de datas.

1. Defina padrões de exibição, validação e edição para o componente do seletor de datas. Além disso, defina uma mensagem de erro de validação personalizada. Por exemplo, você especificou uma data inválida. O formato correto da data é AAAA-MM-DD.

1. Defina o texto de acessibilidade personalizado para o componente seletor de datas. Por exemplo, insira sua data de nascimento. Leitores de tela leem esses textos de acessibilidade personalizados.

1. Use descrição curta em vez de descrição longa para componentes de formulário adaptáveis. Uma descrição longa adiciona o botão de ajuda. Verifique se o formulário adaptável não tem nenhum botão de ajuda.

1. Adicione texto de acessibilidade personalizado a todas as células de tabelas somente leitura. Além disso, desative todas as células somente leitura das tabelas.

1. Remova os campos de assinatura do rabisco, se houver, no formulário adaptável. Configure o formulário adaptável para usar o Adobe Sign para uma experiência de assinatura digital contínua.

### 2. Fornecer rótulos adequados para controles de formulário {#provide-proper-labels-for-form-controls}

O rótulo ou o título de um componente identifica o que o componente de formulário representa. Por exemplo, o texto &quot;Nome&quot; informa aos usuários que eles devem inserir seu nome em um campo de texto. Para ser acessível por leitores de tela, o rótulo é associado de forma programática a um componente de formulário. Como alternativa, o controle de formulário é configurado com informações adicionais de acessibilidade.

O rótulo percebido pelos leitores de tela não precisa ser necessariamente o mesmo da legenda visual. Em alguns casos, talvez você queira ser mais específico sobre a finalidade do controle. Para cada objeto de campo em um formulário, as opções de acessibilidade podem ser usadas para especificar o que o leitor de tela anuncia para identificar o campo de formulário específico.

Para usar a opção Acessibilidade , siga estas etapas:

1. Selecione um componente e toque em ![cmppr](assets/cmppr.png).
1. Clique em **[!UICONTROL Acessibilidade]** na barra lateral para escolher a opção de acessibilidade desejada.

### Opções de acessibilidade em componentes de formulário {#accessibility-options-in-form-components}

![Opções de acessibilidade em componentes de formulário](assets/accessibility-options.png)

**Texto personalizado** Os autores de formulários fornecem o conteúdo na opção acessibilidade Campo de texto personalizado. A tecnologia de assistência, como leitores de tela, usa esse texto personalizado. Usar a configuração de Título é a melhor opção na maioria dos cenários. Considere criar Reader de tela personalizada somente texto ao usar o Título ou uma breve descrição não é possível.

**Descrição curta** Para a maioria dos componentes, a breve descrição é exibida no tempo de execução, quando o usuário passa o ponteiro sobre o componente. É possível definir essa opção no campo de descrição curta, na opção de conteúdo da ajuda.

**Título** Use essa opção para permitir que o AEM Forms use o rótulo visual associado ao campo de formulário como o texto do leitor de tela.

**Nome** Você pode especificar um valor no campo Nome da guia Vínculo. O nome não pode conter espaços.

**Nenhum** Selecionar Nenhum faz com que o objeto de formulário não tenha um nome no formulário publicado. Nenhum não é uma configuração recomendada para controles de formulário.

>[!NOTE]
>
>* Botão de opção e caixa de seleção podem ter apenas duas opções de acessibilidade, a saber, Texto personalizado e Título.
>* Para formulários adaptáveis baseados em XFA, a opção de acessibilidade é herdada das opções de acessibilidade definidas no XDP. Dicas de ferramentas do XDP são mapeadas para a Descrição curta e a Legenda são mapeadas para o Título. As outras opções funcionam como estão.


### 3. Fornecer equivalentes de texto para imagens {#provide-text-equivalents-for-images}

As imagens podem ajudar a melhorar a compreensão para alguns usuários. No entanto, para usuários que usam leitores de tela, as imagens diminuem a acessibilidade de seu formulário. Se você optar por usar imagens, forneça descrições de texto para todas as imagens.

O texto deve descrever o objeto e sua finalidade no formulário. Um leitor de tela lê esse texto alternativo quando encontra uma imagem. Uma imagem deve sempre ter um texto alternativo especificado.

Selecione um componente de imagem e toque em ![cmppr](assets/cmppr.png). Na barra lateral, em Propriedades, especifique o texto alternativo para uma imagem.

![Texto alternativo para uma imagem](assets/image-properties.png)

### 4. Fornecer contraste de cor suficiente {#provide-sufficient-color-contrast}

O design de acessibilidade envolve considerar diretrizes adicionais para o uso de cores. Os autores de formulários podem usar cores para melhorar a aparência dos formulários, destacando vários componentes de formulário. No entanto, um uso impróprio da cor pode tornar um formulário difícil ou impossível de ser lido por pessoas com habilidades diferentes.

Os usuários portadores de deficiência visual dependem de um alto contraste entre o texto e o plano de fundo para ler o conteúdo digital. Sem contraste suficiente, um formulário pode se tornar difícil, se não impossível, de ler para alguns usuários.

É recomendável usar as cores padrão de fonte e plano de fundo — conteúdo em preto em um plano de fundo branco. Se você alterar as cores padrão, escolha uma cor de primeiro plano escura em uma cor de plano de fundo clara ou vice-versa.

Consulte [Criar temas personalizados para formulários adaptáveis](/help/forms/using/creating-custom-adaptive-form-themes.md), para obter mais informações sobre como alterar o contraste de cores e o tema dos formulários adaptáveis.

### 5. Certifique-se de que os controles de formulário sejam acessíveis pelo teclado {#ensure-that-form-controls-are-keyboard-accessible}

Um formulário acessível pode ser preenchido completamente usando apenas o teclado ou um dispositivo de entrada equivalente. Usuários com mobilidade reduzida ou visão deficiente podem não ter escolha senão usar o teclado e muitos usuários que podem usar um mouse, preferir a entrada do teclado. Ao permitir os vários métodos de entrada, você não apenas cria formulários acessíveis, como também cria formulários mais adequados para as preferências de todos os usuários.

Os seguintes atalhos de teclado estão disponíveis no AEM Forms.

| Ação | Atalho de teclado |
|---|---|
| Mover o cursor para frente em um formulário | Guia |
| Mover o cursor para trás em um formulário | Shift+Tab |
| Mover para o próximo painel | Alt+Seta para a direita |
| Mover para o painel anterior | Alt+Seta para a esquerda |
| Redefinir os dados preenchidos em um formulário | Alt+R |
| Enviar um formulário | Alt+S |

Além disso, há várias teclas de atalho de teclado disponíveis para a variável **[!UICONTROL Seletor de data]** no Adaptive Forms. Para ativar as teclas de atalho, toque no **[!UICONTROL Seletor de data]** componente e toque ![Configurar](assets/configure-icon.svg) para abrir as propriedades. No **[!UICONTROL Padrões]** selecione um padrão de exibição usando a **[!UICONTROL Tipo]** e **[!UICONTROL Padrão]** listas suspensas. Salve as propriedades para ativar o uso de teclas de atalho para a variável **[!UICONTROL Seletor de data]** componente.

As seguintes teclas de atalho do teclado estão disponíveis para o componente Seletor de data no Adaptive Forms:

| Ação | Atalho de teclado |
|---|---|
| <ul><li>Exibir as opções do componente Seletor de datas quando o foco da guia realçar o ícone do calendário</li><li>Executar o evento de clique quando o foco da guia realçar uma opção</li> | Espaço ou Enter |
| Ocultar as opções do componente Seletor de datas | Esc |
| <ul><li>Mova o cursor para frente por meio das opções disponíveis no componente Seletor de datas.</li><li>Definir foco da guia no ícone de calendário quando o campo de entrada de data estiver ativo</li> | Guia |
| Mova o cursor para trás através das opções disponíveis no componente Seletor de datas | Shift+Tab |
| <ul><li>Exibir as opções do componente Seletor de data quando o foco da guia realçar o campo de entrada de data</li><li>Mova o cursor para baixo no calendário disponível no componente Seletor de datas</li> | Seta para baixo |
| Mova o cursor para cima no calendário, disponível no componente Seletor de datas | Seta para cima |
| Move o cursor para trás no calendário, disponível no componente Seletor de datas | Seta para a esquerda |
| Move o cursor para frente no calendário disponível no componente Seletor de datas | Seta para a direita |
| Executar a ação da legenda disponível entre as setas de navegação para a direita e para a esquerda no calendário | Shift+Seta para cima |
| Executar a ação para o ícone de seta de navegação direita ![seta para a direita](assets/right-navigation-icon.svg) disponível no calendário | Shift+Seta para a esquerda |
| Executar a ação para o ícone de seta de navegação à esquerda ![seta esquerda](assets/left-navigation-icon.svg) disponível no calendário | Shift+Seta para a direita |

## Use a ferramenta de acessibilidade para encontrar problemas de acessibilidade restantes

O ANDI (Accessible Name and Description Inspetor) ajuda a identificar e corrigir problemas relacionados à conformidade de acessibilidade em um formulário adaptável. Para usar a ferramenta ANDI para encontrar os problemas de acessibilidade em um formulário adaptável:

1. Abra o formulário adaptável no modo de visualização.
1. Clique no ícone de ferramenta ANDI marcado. A ferramenta ANDI analisa o formulário adaptável e exibe problemas de acessibilidade. Para obter detalhes sobre como usar a ferramenta, consulte [Documentação da ANDI](https://www.ssa.gov/accessibility/andi/help/howtouse.html).
1. Revise e corrija os problemas relatados pela ANDI.
