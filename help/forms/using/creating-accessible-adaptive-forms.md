---
title: Criação de formulários adaptáveis acessíveis
seo-title: Criação de formulários adaptáveis acessíveis
description: O AEM Forms fornece ferramentas e para criar formulários adaptáveis acessíveis, além de ajudar a cumprir os padrões de acessibilidade.
seo-description: O AEM Forms fornece ferramentas e para criar formulários adaptáveis acessíveis, além de ajudar a cumprir os padrões de acessibilidade.
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---


# Criação de formulários adaptáveis acessíveis{#creating-accessible-adaptive-forms}

## Introdução {#introduction}

Um formulário acessível é um formulário que todos podem usar, incluindo usuários com necessidades especiais. Os Formulários adaptativos incluem vários recursos e recursos que melhoram a usabilidade para usuários com diferentes capacidades. A inclusão da acessibilidade em formulários adaptáveis não só permite a maior audiência possível para o conteúdo, como também é um requisito ao fornecer documentos em regiões onde a conformidade com os padrões de acessibilidade é obrigatória. Os AEM Forms ajudam os desenvolvedores a formulários a cumprir os padrões de acessibilidade.

Ao criar um formulário adaptável, o autor deve considerar os seguintes pontos para criar um formulário adaptável acessível:

* Verifique o formulário com a ferramenta de teste de acessibilidade ANDI (Accessible Name and Description Inspetor)
* Fornecer rótulos adequados para controles de formulário
* Fornecer equivalentes de texto para imagens
* Fornecer contraste de cor suficiente
* Verifique se os controles de formulário são acessíveis ao teclado

## Pré-requisitos

Você precisa de uma ferramenta de acessibilidade, como o **Accessible Name and Description Inspetor (ANDI)** e um tema de Formulário **adaptável desenvolvido para corrigir problemas** relacionados à acessibilidade para criar um formulário adaptável acessível.

### Download e instalação da ferramenta de teste de acessibilidade

A ferramenta ANDI (Accessible Name and Description Inspetor) ajuda a identificar e corrigir problemas relacionados à conformidade de acessibilidade no conteúdo da Web. É a ferramenta recomendada sob as diretrizes do Trusted Tester v5 do Department of Homeland Security. É desenvolvido pelo departamento &#x200B; Administração de Segurança Social dos Estados Unidos para verificar a conformidade do conteúdo da Web com a Seção 508. A ferramenta:

* Ajuda a detectar problemas de acessibilidade &#x200B; em uma página da Web
* Fornece sugestões para melhorar a acessibilidade &#x200B;
* Detecta problemas de acessibilidade e contraste de cores do teclado
* Identifica claramente o conteúdo do leitor de tela em conformidade com os padrões

A ANDI funciona com todos os principais navegadores da Internet. Consulte a documentação [da](https://www.ssa.gov/accessibility/andi/help/install.html) ANDI para obter instruções detalhadas sobre como configurar e usar a ferramenta.

### Baixe e instale o tema acessível pelo Ultramarine

O tema Acessibilidade ao ultramarino é um tema de referência. Ele ajuda a demonstrar como corrigir o contraste de cores e outros problemas relacionados à acessibilidade em um formulário adaptável. A Adobe recomenda criar um tema personalizado para o ambiente de produção com base nos estilos aprovados por sua organização. Execute as seguintes etapas para fazer upload do tema para sua instância do AEM:

1. Baixe o pacote do tema.
1. Navegue até **[!UICONTROL Experience Manager]** > **[!UICONTROL Navegação]** ![de navegação](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Formulários]** em sua instância do AEM.
1. Toque em **[!UICONTROL Criar]** > Upload **[!UICONTROL de arquivo]**. Selecione e carregue o arquivo x Ultramarine-Accessible-Theme.zip. Ele carrega o tema para sua instância do AEM.

## Tornar um formulário adaptável acessível

Você deve se concentrar em quatro aspectos principais: navegação no teclado, contraste de cores, texto alternativo significativo para imagens e rótulos adequados para controles de formulários para tornar um formulário adaptável acessível. Execute as seguintes etapas para tornar os formulários adaptativos existentes acessíveis:

### 1. Aplicar um tema acessível e executar correções adicionais

Aplique o tema acessível pelo Ultramarine ao formulário adaptável existente. Para aplicar o tema:

1. Abra o formulário adaptável para edição.
1. Selecione um componente e toque no ícone pai. No menu de contexto, toque em Container **** de formulário adaptável e, em seguida, toque no ícone de configuração.
1. Selecione o tema Acessível ao ultramarine no navegador de propriedades e toque no ícone **[!UICONTROL Salvar]** .
1. Atualize a janela do navegador. O tema é aplicado à forma adaptativa.

Depois de aplicar um tema acessível, execute as correções adicionais listadas abaixo. As correções são adicionais às correções de acessibilidade abordadas no tema acessível:

1. Adicione um texto alternativo significativo para a imagem do logotipo no formulário adaptável.

   Forneça um texto alternativo significativo para imagens nos componentes de cabeçalho e rodapé do modelo de formulário adaptável. Quando você corrige o modelo e o usa para criar um formulário adaptável, os formulários adaptáveis herdam todas as correções relacionadas à acessibilidade aplicadas ao cabeçalho e rodapé do modelo.  Para um formulário adaptável existente, faça alterações no nível do formulário adaptável. As alterações feitas em um modelo de formulário adaptável não fluem automaticamente para um formulário adaptável existente.

1. Adicione um componente de cabeçalho que contém o nome do formulário ao formulário adaptável. Se o design de formulário especificar um nome de empresa, adicione também um componente de cabeçalho separado para o nome da empresa.

   A maioria das ferramentas de acessibilidade informa os usuários sobre a hierarquia do conteúdo para ajudá-los a entender a estrutura da página da Web. Defina diferentes níveis de cabeçalho para o texto do nome da organização e do nome do formulário no formulário adaptável para fornecer uma estrutura hierárquica para esse texto. Além disso, use um componente de Texto antes de cada painel e seção com um nível de cabeçalho apropriado para criar uma hierarquia.

   ![Como aplicar um estilo de cabeçalho](assets/apply-style.gif)

1. Altere a cor de fundo do rodapé para usar o contraste apropriado de acordo com os padrões de acessibilidade para melhorar a visibilidade e a legibilidade do texto. Você pode usar a ANDI para localizar problemas de contraste de cores no formulário. Além disso, não use fontes muito pequenas. Fontes pequenas são difíceis de ler.

1. Substitua os componentes switch e image de escolha no formulário adaptável existente pelo componente de escolha (rádio).

1. Substitua o componente de revisão numérico no formulário adaptável existente por um componente de caixa numérica.

1. Substitua o campo de entrada de data pelo campo seletor de datas.

1. Defina padrões de exibição, validação e edição para o componente do seletor de datas. Além disso, defina uma mensagem de erro de validação personalizada. Por exemplo, você especificou uma data inválida. O formato correto da data é AAAA-MM-DD.

1. Defina o texto de acessibilidade personalizado para o componente seletor de datas. Por exemplo, insira sua data de nascimento. Leitores de tela leem esses textos de acessibilidade personalizados.

1. Use descrição curta em vez de descrição longa para componentes de formulário adaptáveis. Uma descrição longa adiciona o botão de ajuda. Verifique se o formulário adaptável não tem nenhum botão de ajuda.

1. Adicione texto de acessibilidade personalizado a todas as células somente leitura das tabelas. Além disso, desative todas as células somente leitura das tabelas.

1. Remova os campos de assinatura codificáveis, se houver, no formulário adaptável. Configure o formulário adaptável para usar o Adobe Sign para obter uma experiência de assinatura digital contínua.

### 2. Fornecer rótulos adequados para controles de formulário {#provide-proper-labels-for-form-controls}

O rótulo ou o título de um componente identifica o que o componente de formulário representa. Por exemplo, o texto &quot;Nome&quot; informa aos usuários que eles precisam digitar seu nome em um campo de texto. Para ser acessível pelos leitores de tela, o rótulo é associado de forma programática a um componente de formulário. Como alternativa, o controle de formulário é configurado com informações adicionais de acessibilidade.

O rótulo percebido pelos leitores de tela não precisa ser necessariamente o mesmo da legenda visual. Em alguns casos, talvez você queira ser mais específico sobre a finalidade do controle. Para cada objeto de campo em um formulário, as opções de acessibilidade podem ser usadas para especificar o que o leitor de tela anuncia para identificar o campo de formulário específico.

Para usar a opção Acessibilidade, siga estas etapas:

1. Selecione um componente e toque em ![cmppr](assets/cmppr.png).
1. Clique em **[!UICONTROL Acessibilidade]** na barra lateral para escolher a opção de acessibilidade desejada.

### Opções de acessibilidade em componentes de formulário {#accessibility-options-in-form-components}

![Opções de acessibilidade em componentes de formulário](assets/accessibility-options.png)

**Os autores do formulário de texto** personalizado fornecem o conteúdo na opção de acessibilidade Campo de texto Personalizado. A tecnologia de assistência, como leitores de tela, usa esse texto personalizado. Usar a configuração Título é a melhor opção na maioria dos cenários. Considere a criação de Texto personalizado do leitor de tela somente ao usar o Título ou uma breve descrição não é possível.

**Descrição** curta Para a maioria dos componentes, a descrição curta aparece no tempo de execução quando o usuário posiciona o ponteiro sobre o componente. É possível definir essa opção no campo de descrição curta, em opção de conteúdo de ajuda.

**Título** Use essa opção para permitir que os AEM Forms usem o rótulo visual associado ao campo de formulário como o texto do leitor de tela.

**Nome** Você pode especificar um valor no campo Nome da guia Vínculo. O nome não pode conter espaços.

**Nenhum** Selecionar Nenhum faz com que o objeto de formulário não tenha um nome no formulário publicado. Nenhum não é uma configuração recomendada para controles de formulário.

>[!NOTE]
>
>* Botão de opção e caixa de seleção podem ter apenas duas opções para acessibilidade, ou seja, Texto personalizado e Título.
>* Para formulários adaptativos baseados em XFA, a opção de acessibilidade é herdada das opções de acessibilidade definidas no XDP. As dicas de ferramentas do XDP são mapeadas para Descrição curta e Legenda são mapeadas para Título. As outras opções funcionam como estão.


### 3. Fornecer equivalentes de texto para imagens {#provide-text-equivalents-for-images}

As imagens podem ajudar a melhorar a compreensão para alguns usuários. No entanto, para os usuários que usam leitores de tela, as imagens diminuem a acessibilidade do formulário. Se você optar por usar imagens, forneça descrições de texto para todas as imagens.

Verifique se o texto descreve o objeto e sua finalidade no formulário. Um leitor de tela lê esse texto alternativo quando encontra uma imagem. Uma imagem sempre deve ter um texto alternativo especificado.

Selecione um componente de imagem e toque em ![cmppr](assets/cmppr.png). Na barra lateral, em Propriedades, especifique o texto alternativo para uma imagem.

![Texto alternativo para uma imagem](assets/image-properties.png)

### 4. Fornecer contraste de cor suficiente {#provide-sufficient-color-contrast}

O design de acessibilidade envolve considerar diretrizes adicionais para o uso de cores. Os autores de formulários podem usar cores para melhorar a aparência dos formulários, destacando vários componentes do formulário. No entanto, um uso impróprio da cor pode tornar um formulário difícil ou impossível de ler por pessoas com habilidades diferentes.

Os usuários portadores de deficiências visuais dependem de um alto contraste entre o texto e o plano de fundo para ler conteúdo digital. Sem contraste suficiente, um formulário pode se tornar difícil, se não impossível, de ler para alguns usuários.

É recomendável usar as cores padrão de fonte e plano de fundo — conteúdo em preto em um plano de fundo branco. Se você alterar as cores padrão, escolha uma cor escura do primeiro plano em uma cor clara do plano de fundo ou vice-versa.

Consulte [Criar temas personalizados para formulários](/help/forms/using/creating-custom-adaptive-form-themes.md)adaptáveis para obter mais informações sobre como alterar o contraste e o tema das cores para os formulários adaptáveis.

### 5. Verifique se os controles de formulário são acessíveis ao teclado {#ensure-that-form-controls-are-keyboard-accessible}

Um formulário acessível pode ser preenchido completamente usando apenas o teclado ou um dispositivo de entrada equivalente. Usuários com mobilidade reduzida ou visão deficiente podem não ter escolha senão usar o teclado e muitos usuários que podem usar o mouse preferem a entrada do teclado. Ao permitir os vários métodos de entrada, você não só cria formulários acessíveis, como também cria formulários mais adequados às preferências de todos os usuários.

Os seguintes atalhos de teclado estão disponíveis no AEM Forms.

| Ação | Atalho de teclado |
|---|---|
| Mover o cursor para frente em um formulário | Guia |
| Mover o cursor para trás em um formulário | Shift+Tab |
| Mover para o painel seguinte | Alt+Seta para a direita |
| Mover para o painel anterior | Alt+Seta para a esquerda |
| Redefinir os dados preenchidos em um formulário | Alt+R |
| Enviar um formulário | Alt+S |

## Use a ferramenta de acessibilidade para encontrar problemas de acessibilidade restantes

O ANDI (Accessible Name and Description Inspetor) ajuda a identificar e corrigir problemas relacionados à conformidade com acessibilidade em um formulário adaptável. Para usar a ferramenta ANDI para localizar os problemas de acessibilidade em um formulário adaptável:

1. Abra o formulário adaptável no modo de pré-visualização.
1. Clique no ícone da ferramenta ANDI marcada. A ferramenta ANDI analisa o formulário adaptável e exibe problemas de acessibilidade. Para obter detalhes sobre como usar a ferramenta, consulte a documentação [da](https://www.ssa.gov/accessibility/andi/help/howtouse.html)ANDI.
1. Revise e corrija os problemas reportados pela ANDI.