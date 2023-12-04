---
title: Criação de formulários adaptáveis acessíveis
seo-title: Creating accessible adaptive forms
description: O AEM Forms fornece ferramentas e para criar formulários adaptáveis acessíveis, além de ajudar a cumprir os padrões de acessibilidade.
seo-description: AEM Forms provides you tools and to create accessible adaptive forms and helps comply with accessibility standards.
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
feature: Adaptive Forms
exl-id: e755159f-374f-42b8-b28b-e8864df44f9d
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '2099'
ht-degree: 0%

---

# Criação de formulários adaptáveis acessíveis{#creating-accessible-adaptive-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Introdução {#introduction}

Um formulário acessível é um formulário que qualquer pessoa pode usar, incluindo usuários com necessidades especiais. O Forms adaptável inclui vários recursos e funcionalidades que melhoram a usabilidade para usuários com habilidades diferentes. A criação de acessibilidade em formulários adaptáveis não só permite o maior público possível de conteúdo, como também é um requisito ao fornecer documentos em regiões geográficas onde a conformidade com os padrões de acessibilidade é obrigatória. A ajuda dos desenvolvedores de formulários do AEM Forms está em conformidade com os padrões de acessibilidade.

Ao criar um formulário adaptável, o autor deve considerar os seguintes pontos para criar um formulário adaptável acessível:

* Verifique o formulário com a ferramenta de teste de acessibilidade ANDI (Inspetor de nome e descrição acessíveis)
* Fornecer rótulos adequados para controles de formulário
* Fornecer equivalentes de texto para imagens
* Fornecer contraste de cores suficiente
* Garantir que os controles de formulário estejam acessíveis ao teclado

## Pré-requisitos

Você precisa de uma ferramenta de acessibilidade, como **Inspetor de Nome e Descrição Acessível (ANDI)** e uma **Tema do formulário adaptável desenvolvido para corrigir problemas relacionados à acessibilidade** para criar um formulário adaptável acessível.

### Baixar e instalar a ferramenta de teste de acessibilidade

A ferramenta Inspetor de nome e descrição acessíveis (ANDI) ajuda a identificar e corrigir problemas relacionados à conformidade de acessibilidade no conteúdo da Web. É a ferramenta recomendada sob as diretrizes Trusted Tester v5 do Departamento de Segurança Interna. Ele é desenvolvido pelo departamento de Administração de Segurança Social &#x200B; Estados Unidos para verificar a conformidade da Seção 508 do conteúdo da Web. A ferramenta:

* Ajuda a detectar problemas de acessibilidade&#x200B; em uma página da Web
* Fornece sugestões para melhorar a acessibilidade&#x200B;
* Detecta problemas de acessibilidade e contraste de cores do teclado
* Identifica claramente o conteúdo do leitor de tela em conformidade com os padrões

O ANDI funciona com todos os principais navegadores da Internet. Consulte [Documentação da ANDI](https://www.ssa.gov/accessibility/andi/help/install.html) para obter instruções detalhadas sobre como configurar e usar a ferramenta.

### Baixe e instale o tema acessível pelo Ultramarine

O tema acessível a ultramarinos é um tema de referência. Ele ajuda a demonstrar como corrigir o contraste de cores e outros problemas relacionados à acessibilidade em um formulário adaptável. A Adobe recomenda criar um tema personalizado para o ambiente de produção com base nos estilos aprovados por sua organização. Execute as seguintes etapas para fazer upload do tema para sua instância AEM:

1. Baixe o pacote de tema.
1. Navegue até **[!UICONTROL Experience Manager]** > **[!UICONTROL Navegação]** ![Navegação](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]** na sua instância do AEM.
1. Selecionar **[!UICONTROL Criar]** > **[!UICONTROL Upload de arquivo]**. Selecione e faça upload do arquivo x Ultramarine-Accessible-Theme.zip. Ele carrega o tema para sua instância AEM.

## Tornar um formulário adaptável acessível

Você deve se concentrar em quatro aspectos principais: navegação pelo teclado, contraste de cores, texto alternativo significativo para imagens e rótulos apropriados para controles de formulários para tornar um formulário adaptável acessível. Execute as seguintes etapas para tornar acessíveis seus formulários adaptáveis existentes:

### 1. Aplicar um tema acessível e executar correções adicionais

Aplique o tema acessível pelo Ultramarine ao seu formulário adaptável existente. Para aplicar o tema:

1. Abra o formulário adaptável para edição.
1. Selecione um componente e selecione o ícone pai. No menu de contexto, selecione **[!UICONTROL Contêiner de formulário adaptável]** e, em seguida, selecione o ícone configurar.
1. Selecione o tema acessível por ultramarinos no navegador de propriedades e selecione **[!UICONTROL Salvar]** ícone.
1. Atualize a janela do navegador. O tema é aplicado ao formulário adaptável.

Depois de aplicar um tema acessível, execute as correções adicionais listadas abaixo. As correções estão além das correções de acessibilidade abordadas no tema acessível:

1. Adicione um texto alternativo significativo para a imagem do logotipo no formulário adaptável.

   Forneça um texto alternativo significativo para imagens nos componentes de cabeçalho e rodapé do modelo de formulário adaptável. Quando você corrige o modelo e o usa para criar um formulário adaptável, os formulários adaptáveis herdam todas as correções relacionadas à acessibilidade aplicadas ao cabeçalho e ao rodapé do modelo.  Para um formulário adaptável existente, faça alterações no nível do formulário adaptável. As alterações feitas em um modelo de formulário adaptável não fluem automaticamente para um formulário adaptável existente.

1. Adicione um componente de cabeçalho que contenha o nome do formulário ao formulário adaptável. Se o design do formulário especificar um nome de empresa, adicione também um componente de cabeçalho separado para o nome da empresa.

   A maioria das ferramentas de acessibilidade informa os usuários sobre a hierarquia do conteúdo para ajudá-los a entender a estrutura da página da Web. Defina diferentes níveis de cabeçalho para o nome da organização e o texto do nome do formulário no formulário adaptável para fornecer uma estrutura hierárquica a esses textos. Além disso, use um componente de Texto antes de cada painel e seção com um nível de cabeçalho apropriado para criar uma hierarquia.

   ![Como aplicar um estilo de cabeçalho](assets/apply-style.gif)

1. Altere a cor do plano de fundo do rodapé para usar o contraste apropriado de acordo com os padrões de acessibilidade para melhorar a visibilidade e a legibilidade do texto. Você pode usar ANDI para encontrar problemas de contraste de cor em seu formulário. Além disso, não use fontes muito pequenas. Fontes pequenas são difíceis de ler.

1. Substitua o switch e os componentes de escolha de imagem em seu formulário adaptável existente pelo componente de escolha (rádio).

1. Substitua o componente de passo numérico em seu formulário adaptável existente pelo componente de caixa numérica.

1. Substituir o campo de entrada de data pelo campo seletor de datas.

1. Defina os padrões de exibição, validação e edição para o componente seletor de datas. Além disso, defina uma mensagem de erro de validação personalizada. Por exemplo, Você especificou uma data inválida. O formato correto da data é AAAA-MM-DD.

1. Defina o texto de acessibilidade personalizado para o componente seletor de datas. Por exemplo, insira sua data de nascimento. Os leitores de tela leem esses textos de acessibilidade personalizados.

1. Use descrição curta em vez de descrição longa para componentes de formulário adaptáveis. Uma descrição longa adiciona o botão de ajuda. Verifique se a área adaptável não tem nenhum botão de ajuda.

1. Adicione um texto de acessibilidade personalizado a todas as células somente leitura das tabelas. Além disso, desative todas as células somente leitura das tabelas.

1. Remova os campos de assinatura rabisco, se houver, no formulário adaptável. Configure o formulário adaptável para usar o Adobe Sign e obter uma experiência de assinatura digital contínua.

### 2. Fornecer rótulos adequados para controles de formulário {#provide-proper-labels-for-form-controls}

O rótulo ou título de um componente identifica o que o componente de formulário representa. Por exemplo, o texto &quot;Nome&quot; informa aos usuários que eles devem inserir seu nome em um campo de texto. Para ser acessível por leitores de tela, o rótulo é associado programaticamente a um componente de formulário. Como alternativa, o controle de formulário é configurado com informações adicionais de acessibilidade.

O rótulo percebido pelos leitores de tela não precisa necessariamente ser o mesmo da legenda visual. Em alguns casos, talvez você queira ser mais específico sobre a finalidade do controle. Para cada objeto de campo em um formulário, as opções de acessibilidade podem ser usadas para especificar o que o leitor de tela anuncia para identificar o campo de formulário específico.

Para usar a opção Acessibilidade, siga estas etapas:

1. Selecione um componente e selecione ![cmppr](assets/cmppr.png).
1. Clique em **[!UICONTROL Acessibilidade]** na barra lateral para escolher a opção de acessibilidade desejada.

### Opções de acessibilidade em componentes de formulário {#accessibility-options-in-form-components}

![Opções de acessibilidade em componentes de formulário](assets/accessibility-options.png)

**Texto personalizado** Os autores do formulário fornecem o conteúdo na opção de acessibilidade Campo de texto personalizado. A tecnologia assistiva, como leitores de tela, usa esse texto personalizado. O uso da configuração de Título é a melhor opção na maioria dos cenários. Considere a criação de Texto de Reader de tela personalizada somente ao usar o Título ou se não for possível usar uma descrição curta.

**Descrição curta** Para a maioria dos componentes, a breve descrição aparece no tempo de execução quando o usuário passa o ponteiro do mouse sobre o componente. É possível definir essa opção no campo de descrição curta, na opção conteúdo da ajuda.

**Título** Use essa opção para permitir que o AEM Forms use o rótulo visual associado ao campo de formulário como o texto do leitor de tela.

**Nome** Você pode especificar um valor no campo Nome da guia Vinculação. O nome não pode conter espaços.

**Nenhum** Selecionar Nenhum faz com que o objeto de formulário não tenha um nome no formulário publicado. Nenhum não é uma configuração recomendada para controles de formulário.

>[!NOTE]
>
>* O botão de opção e a caixa de seleção podem ter apenas duas opções de acessibilidade, a saber, Texto personalizado e Título.
>* Para formulários adaptáveis baseados em XFA, a opção de acessibilidade é herdada das opções de acessibilidade definidas no XDP. As dicas de ferramentas do XDP são mapeadas de acordo com a Descrição curta e a Legenda são mapeadas de acordo com o Título. As outras opções funcionam como estão.

### 3. Fornecer equivalentes de texto para imagens {#provide-text-equivalents-for-images}

As imagens podem ajudar a melhorar a compreensão de alguns usuários. No entanto, para usuários que usam leitores de tela, as imagens reduzem a acessibilidade do formulário. Se você optar por usar imagens, forneça descrições de texto para todas as imagens.

Certifique-se de que o texto descreve o objeto e sua finalidade no formulário. Um leitor de tela lê esse texto alternativo quando encontra uma imagem. Uma imagem deve sempre ter um texto alternativo especificado.

Selecione um componente de imagem e selecione ![cmppr](assets/cmppr.png). Na barra lateral, em Propriedades, especifique o texto alternativo para uma imagem.

![Texto alternativo para uma imagem](assets/image-properties.png)

### 4. Fornecer contraste de cor suficiente {#provide-sufficient-color-contrast}

O design de acessibilidade envolve considerar diretrizes adicionais para o uso de cores. Os autores de formulários podem usar cores para melhorar a aparência dos formulários, destacando vários componentes de formulário. No entanto, o uso inadequado da cor pode dificultar ou impossibilitar a leitura de uma forma por pessoas com diferentes habilidades.

Os usuários com deficiências visuais dependem de um alto contraste entre o texto e o plano de fundo para ler o conteúdo digital. Sem contraste suficiente, um formulário pode se tornar difícil, se não impossível, de ser lido para alguns usuários.

É recomendável usar a fonte padrão e as cores de fundo — conteúdo na cor preta em um plano de fundo branco. Se você alterar as cores padrão, escolha uma cor de primeiro plano escura em uma cor de fundo clara ou vice-versa.

Consulte [Criação de temas personalizados para formulários adaptáveis](/help/forms/using/creating-custom-adaptive-form-themes.md), para obter mais informações sobre como alterar o contraste e o tema da cor dos formulários adaptáveis.

### 5. Verifique se os controles de formulário estão acessíveis ao teclado {#ensure-that-form-controls-are-keyboard-accessible}

Um formulário acessível pode ser preenchido completamente usando apenas o teclado ou um dispositivo de entrada equivalente. Os usuários com mobilidade reduzida ou visão prejudicada podem não ter outra escolha a não ser usar o teclado e muitos usuários que podem usar um mouse preferem a entrada pelo teclado. Ao permitir os vários métodos de entrada, você não apenas cria formulários acessíveis, mas também cria formulários mais adequados às preferências de todos os usuários.

Os seguintes atalhos de teclado estão disponíveis no AEM Forms.

| Ação | Atalho de teclado |
|---|---|
| Mover o cursor adiante através de um formulário | Guia |
| Mover o cursor para trás em um formulário | Shift+Tab |
| Mover para o próximo painel | Alt+Seta para a Direita |
| Mover para o painel anterior | Alt+Seta para a esquerda |
| Redefinir os dados preenchidos em um formulário | Alt+R |
| Enviar um formulário | Alt+S |

Além disso, há várias teclas de atalho de teclado disponíveis para o **[!UICONTROL Seletor de data]** no Forms adaptável. Para ativar as teclas de atalho, selecione a **[!UICONTROL Seletor de data]** e selecione ![Configurar](assets/configure-icon.svg) para abrir as propriedades. No **[!UICONTROL Padrões]** selecione um padrão de exibição usando a variável **[!UICONTROL Tipo]** e **[!UICONTROL Padrão]** listas suspensas. Salve as propriedades para permitir o uso de teclas de atalho para o **[!UICONTROL Seletor de data]** componente.

As seguintes teclas de atalho de teclado estão disponíveis para o componente Seletor de datas no Adaptive Forms:

| Ação | Atalho de teclado |
|---|---|
| <ul><li>Exibir as opções do componente Seletor de datas quando o foco da guia realçar o ícone do calendário</li><li>Execute o evento de clique quando o foco da guia realçar uma opção</li> | Space ou Enter |
| Ocultar as opções do componente Seletor de datas | Esc |
| <ul><li>Mova o cursor para frente pelas opções disponíveis no componente Seletor de datas.</li><li>Definir o foco da guia no ícone do calendário quando o campo de entrada de data estiver ativo</li> | Guia |
| Mova o cursor para trás pelas opções disponíveis no componente Seletor de datas | Shift+Tab |
| <ul><li>Exibir as opções do componente Seletor de datas quando o foco da guia destacar o campo de entrada de data</li><li>Mova o cursor para baixo no calendário disponível no componente Seletor de datas</li> | Seta para baixo |
| Mova o cursor para cima no calendário disponível no componente Seletor de datas | Seta para cima |
| Mova o cursor para trás no calendário disponível no componente Seletor de datas | Seta para a esquerda |
| Mova o cursor para frente no calendário disponível no componente Seletor de datas | Seta para a direita |
| Executar a ação da legenda disponível entre as setas de navegação direita e esquerda no calendário | Shift + Seta para cima |
| Executar a ação para o ícone de seta de navegação direita ![seta para a direita](assets/right-navigation-icon.svg) disponível no calendário | Shift+Seta para a Esquerda |
| Executar a ação para o ícone de seta de navegação à esquerda ![seta para a esquerda](assets/left-navigation-icon.svg) disponível no calendário | Shift + seta para a direita |

## Use a ferramenta de acessibilidade para encontrar problemas de acessibilidade restantes

O Inspetor de nome e descrição acessíveis (ANDI) ajuda a identificar e corrigir problemas relacionados à conformidade de acessibilidade em um formulário adaptável. Para usar a ferramenta ANDI para encontrar os problemas de acessibilidade em um formulário adaptável:

1. Abra o formulário adaptável no modo de visualização.
1. Clique no ícone da ferramenta ANDI marcado. A ferramenta ANDI analisa o formulário adaptável e exibe problemas de acessibilidade. Para obter detalhes sobre como usar a ferramenta, consulte [Documentação da ANDI](https://www.ssa.gov/accessibility/andi/help/howtouse.html).
1. Revise e corrija os problemas relatados por ANDI.
