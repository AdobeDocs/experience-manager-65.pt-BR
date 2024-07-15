---
title: Práticas recomendadas para criar formulários no designer de formulários
description: Saiba mais sobre as práticas recomendadas de acessibilidade para criar formulários no designer de formulários
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 6b86212a2b3a86b2205714c802dc1581d30e7441
workflow-type: tm+mt
source-wordcount: '11687'
ht-degree: 0%

---

# Práticas recomendadas para criar formulários no designer de formulários

O LiveCycle Designer permite criar conteúdo de formulário avançado e cumprir as diretrizes da Seção 508. Este guia contém uma visão geral das práticas recomendadas para criar um formulário acessível e diretrizes para implementar essas práticas recomendadas usando o LiveCycle Designer. As seguintes práticas recomendadas são abordadas:

1. [Mantenha os formulários simples e fáceis de usar](#keep-simple)
1. [Configurar propriedades do formulário para gerar informações de acessibilidade](#configure-form-properties)
1. [Escolha os controles certos](#choose-right-controls)
1. [Fornecer equivalentes de texto para imagens](#provide-text-equivalents)
1. [Fornecer rótulos adequados para controles de formulário](#provide-proper-labels)
1. [Verifique se a leitura e a ordem das guias estão corretas](#ensure-reading-tab-order)
1. [Garantir que os controles de formulário estejam acessíveis ao teclado](#ensure-keyboard-accessible)
1. [Usar a cor com responsabilidade](#use-color-responsibly)
1. [Fornecer células de cabeçalho para tabelas](#provide-heading-cells)
1. [Fornecer uma estrutura de formulário navegável](#provide-navigable-form)
1. [Evitar scripts com interrupções](#avoid-disruptive-scripting)
1. [Verifique se todo o conteúdo de áudio e vídeo está acessível](#ensure-audio-video-accessible)
1. [Identificar o idioma natural e quaisquer alterações no idioma](#identify-natural-language)

## Mantenha os formulários simples e fáceis de usar {#keep-simple}

Um formulário não é acessível se não for fácil de usar. Você deve tentar criar formulários simples e utilizáveis. Um layout simples de controles e campos com legendas claras e relevantes e dicas de ferramentas facilitará o uso do formulário por todos os usuários.
O design de formulários organizado de forma lógica e organizada, que forneça instruções claras e simples, ajudará todos os usuários a preencher formulários da maneira mais fácil possível. Os recursos de navegação, como a ordem de tabulação e os atalhos de teclado, devem oferecer suporte à ordem lógica dos objetos no formulário.

### Evite mover, piscar ou piscar o conteúdo

Alguns indivíduos com epilepsia fotossensível podem ter uma convulsão desencadeada por movimento em frequências superiores a 2 Hz (1 Hz, ou Hertz, igual a um por segundo) e inferiores a 55 Hz (55 por segundo).

O movimento em menos de 2 Hz é considerado lento o suficiente para ser seguro para indivíduos com epilepsia fotossensível. O movimento em mais de 55 Hz é considerado não perceptível.

Os desenvolvedores devem estar cientes desses parâmetros ao usar qualquer movimento no conteúdo da Web.

Outros usuários podem ter deficiências cognitivas que dificultam a concentração quando há conteúdo animado ou intermitente presente no formulário.

Em geral, tente evitar o uso de efeitos óticos inseridos por scripts, como texto ou animação piscando, em formulários interativos. Esses efeitos reduzem a usabilidade dos formulários para determinados usuários.

Pontos de verificação relacionados
* Seção 508 §11934.21

   * h) Quando a animação é exibida, a informação deve ser apresentada em, pelo menos, um modo de apresentação não animado, por opção do utilizador.
   * k) Osoftwarenão deve utilizar textos, objetos ou outros elementos intermitentes ou intermitentes com uma frequência de intermitência superior a 2 Hz e inferior a 55 Hz.
* Seção 508 §11934.22
   * j) As páginas devem ser concebidas de modo a evitar que o ecrã cintile com uma frequência superior a 2 Hz e inferior a 55 Hz.
* WCAG 1.0
   * 7.1 Até que os agentes do usuário permitam que os usuários controlem a oscilação, evite fazer com que a tela pisque. (P1)
   * 7.2 Até que os agentes do usuário permitam que os usuários controlem a intermitência, evite fazer com que o conteúdo intermita (ou seja, altere a apresentação regularmente, como ativar e desativar) (P2).
   * 7.3 Até que os agentes do usuário permitam que os usuários congelem o conteúdo em movimento, evite a movimentação nas páginas.
   * 14.1 Use a linguagem mais clara e simples apropriada para o conteúdo de um site.
* WCAG 2.0
   * 2.2.2 Pausar, Interromper, Ocultar: para mover, piscar, rolar ou atualizar automaticamente as informações, todos os itens a seguir são verdadeiros: (Nível A)
   * 2.3.1 Três Flashes ou Abaixo do limite: as páginas da Web não contêm nada que pisque mais de três vezes em um período de um segundo, ou o flash está abaixo dos limites gerais de flash e flash vermelho. (Nível A)
   * 2.3.2 Três Flashes: as páginas da Web não contêm nada que pisque mais de três vezes em um período de um segundo. (Nível AAA)


## Configurar propriedades do formulário para gerar informações de acessibilidade {#configure-form-properties}

Para que um formulário seja acessível, ele deve ser [perceptível](https://www.w3.org/TR/WCAG20/#perceivable) pela tecnologia assistiva. Por exemplo, a maioria dos leitores de tela não considera o layout visual do formulário, mas a estrutura subjacente.

Para implementar essa estrutura subjacente usando o LiveCycle Designer, você deve criar um formulário PDF com informações de acessibilidade (às vezes chamadas de tags) incluídas, para que o leitor de tela ou outra tecnologia de assistência possa ler o texto e os componentes do formulário. Em um formulário com informações de acessibilidade, cada elemento contém informações sobre sua própria estrutura, além de informações sobre como ele está relacionado ou depende de outros elementos. Somente em arquivos PDF com informações de acessibilidade incluídas os leitores de tela podem identificar e descrever o conteúdo de um documento com precisão.

Para criar um formulário acessível, você deve configurar as propriedades do formulário para que o LiveCycle Designer gere informações de acessibilidade ao salvar o design do formulário como um arquivo PDF:
1. Escolha Arquivo > Propriedades do formulário.
1. Clique na guia Salvar opções e, na área PDF, verifique se a opção Gerar informações de acessibilidade (tags) para Acrobat está selecionada.
1. Clique em OK.

No LiveCycle Designer, essa opção é selecionada por padrão.

>[!NOTE]
> Essas opções só se aplicam ao salvar o design do formulário como um arquivo PDF. Eles não se aplicam aos arquivos PDF criados com o LiveCycle Forms que tem opções de configuração independentes dessa opção no LiveCycle Designer.

**Pontos de verificação relacionados**

* Seção 508 §1194.21
   * d) As tecnologias de assistência devem dispor de informações suficientes sobre um elemento da interface do utilizador, incluindo a identidade, o funcionamento e o estado do elemento. Quando uma imagem representa um elemento de programa, as informações transmitidas pela imagem também devem estar disponíveis no texto.
   * l) Quando forem utilizados formulários eletrônicos, o formulário deve permitir que as pessoas que utilizam a tecnologia assistiva tenham acesso às informações, aos elementos de campo e à funcionalidade necessários para o preenchimento e envio do formulário, incluindo todas as direções e indicações.
* Seção 508 §1194.22
   * n) Quando os formulários eletrônicos são concebidos para serem preenchidos em linha, o formulário deve permitir que as pessoas que utilizam a tecnologia de assistência acedam às informações, aos elementos de campo e à funcionalidade necessários para o preenchimento e envio do formulário, incluindo todas as direções e indicações.


## Escolha os controles certos {#choose-right-controls}

Ao criar seus formulários, use objetos de desenvolvimento nas guias disponíveis na Biblioteca de objetos do LiveCycle Designer. Para exibir esse painel, escolha Janela > Biblioteca de objetos ou pressione Shift+F12 (veja a Figura 1).

![Painel da Biblioteca de Objetos](/help/forms/using/assets/image-1.png)

Figura 1: **Painel da biblioteca de objetos**

Se você usar outros objetos, eles poderão ser ignorados pela tecnologia assistiva. Usar somente os objetos padrão poupa o esforço adicional de definir propriedades de acessibilidade para os objetos que você mesmo criou. Se você criar e usar seus próprios objetos personalizados, certifique-se de usar a paleta Acessibilidade para definir propriedades de acessibilidade, como Função, Dica de ferramenta, Precedência de Reader de tela e Texto Reader de tela personalizado. Para mostrar a paleta Acessibilidade, escolha Janela > Acessibilidade.

**Pontos de verificação relacionados**
* Seção 508 §1194.21
   * c) Deve ser fornecida no ecrã uma indicação bem definida do foco atual que se desloca entre elementos da interface interativa à medida que o foco de entrada muda. O foco deve ser exposto de forma programática para que a tecnologia assistiva possa rastrear as alterações de foco e foco.
   * d) As tecnologias de assistência devem dispor de informações suficientes sobre um elemento da interface do utilizador, incluindo a identidade, o funcionamento e o estado do elemento. Quando uma imagem representa um elemento de programa, as informações transmitidas pela imagem também devem estar disponíveis no texto.
   * l) Quando forem utilizados formulários eletrônicos, o formulário deve permitir que as pessoas que utilizam a tecnologia assistiva tenham acesso às informações, aos elementos de campo e à funcionalidade necessários para o preenchimento e envio do formulário, incluindo todas as direções e indicações.
* Seção 508 §1194.22
   * n) Quando os formulários eletrônicos são concebidos para serem preenchidos em linha, o formulário deve permitir que as pessoas que utilizam a tecnologia de assistência acedam às informações, aos elementos de campo e à funcionalidade necessários para o preenchimento e envio do formulário, incluindo todas as direções e indicações.

* WCAG 2.0
   * 3.2.4 Identificação consistente: os componentes com a mesma funcionalidade em um conjunto de páginas da Web são identificados consistentemente. (Nível AA).
   * 4.1.2 Nome, função, valor: para todos os componentes da interface do usuário (incluindo, mas não limitados a: elementos de formulário, links e componentes gerados por scripts), o nome e a função podem ser determinados de forma programática; estados, propriedades e valores que podem ser definidos pelo usuário podem ser definidos de forma programática; e a notificação de alterações nesses itens está disponível aos agentes do usuário, incluindo tecnologias assistivas. (Nível A)


## Fornecer equivalentes de texto para imagens {#provide-text-equivalents}

As imagens podem ajudar a melhorar a compreensão para usuários com alguns tipos de deficiências. No entanto, para usuários de leitores de tela, as imagens reduzirão a acessibilidade do formulário se você não fornecer uma alternativa textual.

Se você optar por usar imagens, forneça descrições de texto para todos os objetos de imagem e de campo de imagem. Verifique se o texto descreve o objeto e sua finalidade no formulário. Ao definir uma alternativa em texto, o leitor de tela lerá essa alternativa ao encontrar a imagem. Por esse motivo, uma imagem contendo informações sempre deve ter uma alternativa em texto especificada.

Você fornece descrições de texto usando as propriedades Dica de ferramenta ou Texto de Reader de tela personalizado na paleta Acessibilidade ou por meio de campos de texto, legendas e nomes de objeto, conforme especificado na opção Nome da guia Associação. Por exemplo, a Figura 2 mostra um exemplo de uma imagem que contém o texto &quot;Obter Adobe Reader&quot;. Como um leitor de tela não consegue ler o texto que faz parte de uma imagem, você deve incluir uma alternativa de texto no campo Texto de Reader da tela personalizada na paleta Acessibilidade desse objeto. Na maioria dos casos, o texto alternativo deve ser o mesmo que o texto visível na imagem (consulte a Figura 2).

![Especificando texto alternativo para uma imagem usando a paleta Acessibilidade](/help/forms/using/assets/image-2.png)

Figura 2: **Especificando texto alternativo para uma imagem usando a paleta Acessibilidade**

Ao especificar o texto alternativo, considere o seguinte:
* Se o objeto de imagem ou a imagem digitalizada incluir informações importantes para o formulário, crie texto para a imagem na paleta Acessibilidade, que descreve o objeto e sua finalidade. O texto para um logotipo de empresa, por exemplo, pode consistir nas palavras &quot;logotipo de empresa&quot; e o nome da empresa.
* Se o objeto de imagem contiver informações de cor semântica, inclua isso na descrição também. Uma descrição de um semáforo verde, por exemplo, poderia ser &quot;Transmissão bem-sucedida&quot; e a descrição de um sinal vermelho poderia ser &quot;Transmissão falhou&quot;.
* Se você usar gráficos complexos, como gráficos de barras, forneça as informações em uma versão alternativa acessível, como uma tabela ou descrição textual mais longa.
* Não crie descrições de texto para imagens estáticas usadas apenas para decoração.
* Não use os dados digitalizados como informações em segundo plano. Isso pode acontecer quando um designer digitaliza um formulário impresso e usa o Adobe LiveCycle Designer para adicionar novos campos ao formulário. Os leitores de tela não podem detectar os dados digitalizados nesse estado.

Ao incluir conteúdo gráfico meramente decorativo em seus formulários, você deseja garantir que os leitores de tela não anunciem a presença da imagem. Para a maioria dos leitores de tela, isso pode ser feito definindo a propriedade Texto do Reader de tela como Nenhum na paleta Acessibilidade. Se você não fizer isso, alguns leitores de tela poderão anunciar a presença de um gráfico, sem indicar o que ele representa. Para imagens dinâmicas, como objetos de campo de imagem, certifique-se de que as alternativas em texto sejam atualizadas corretamente quando a imagem for alterada. Não crie descrições de texto para objetos de campo de imagem que são usados apenas para decoração. Você pode usar a linguagem de script FormCalc para atribuir descrições de texto a um objeto de campo de imagem dinamicamente. FormCalc é a linguagem de script padrão do Adobe LiveCycle Designer. Por exemplo, considere um formulário com um campo de imagem chamado ImageField1 e o texto associado no nó imagetext dos dados de tempo de execução. Você pode usar scripts para passar esse texto em um evento apropriado (como `form:ready`) da seguinte maneira:

`ImageField1.assist.toolTip = $record.imagetext.value`

Pontos de verificação relacionados
* Seção 508 §1194.22
   * a) Deve ser fornecido um equivalente em texto para cada elemento não textual (por exemplo, através de &quot;alt&quot;, &quot;longdesc&quot; ou no conteúdo do elemento).
* WCAG 1.0
   * 1.1 Forneça um equivalente em texto para cada elemento não textual (por exemplo, por meio de &quot;alt&quot;, &quot;longdesc&quot; ou no conteúdo do elemento). Isso inclui: imagens, representações gráficas de texto (incluindo símbolos), regiões de mapa de imagem, animações (por exemplo, GIF animados), applets e objetos programáticos, arte ascii, quadros, scripts, imagens usadas como marcadores de lista, espaçadores, botões gráficos, sons (reproduzidos com ou sem interação do usuário), arquivos de áudio independentes, faixas de áudio de vídeo e vídeo (P1).
* WCAG 2.0
   * 1.1.1 Conteúdo não textual: todo o conteúdo não textual que é apresentado ao usuário tem uma alternativa em texto que serve um propósito equivalente, exceto para as situações listadas abaixo. (Nível A)


## Fornecer rótulos adequados para controles de formulário{#provide-proper-labels}

O rótulo ou a legenda de um controle de formulário identifica o que o controle de formulário deve representar. Por exemplo, o texto &quot;Nome&quot; informa aos usuários que eles devem inserir seu nome em um campo de texto. Para ser acessível por leitores de tela, o rótulo deve ser associado programaticamente ao controle de formulário ou o controle de formulário deve ser configurado com informações de acessibilidade adicionais usando a paleta Acessibilidade; não é suficiente apenas colocar um objeto de texto ao lado do controle. Para usuários com deficiências visuais, é importante que o rótulo esteja posicionado corretamente ao lado do controle. Ambas as técnicas serão discutidas nas seções a seguir.

### Especificação de texto de rótulo acessível usando a paleta Acessibilidade

O rótulo percebido pelos usuários de leitores de tela não precisa necessariamente ser o mesmo da legenda visual. Em alguns casos, talvez você queira ser mais específico sobre a finalidade do controle.
Para cada objeto de campo em um formulário, a paleta Acessibilidade (veja a Figura 3) pode ser usada para especificar o que o leitor de tela anunciará para identificar o campo de formulário específico.
Para usar a paleta Acessibilidade, siga estas etapas:
1. Exiba a paleta Acessibilidade escolhendo Janela > Acessibilidade ou pressionando Shift+F6.
1. Selecione um objeto no formulário. A paleta mostrará as propriedades de acessibilidade do objeto.

![A paleta de Acessibilidade](/help/forms/using/assets/image-3.png)

Figura 3: **Paleta de acessibilidade**

Quando o formulário é salvo como um PDF, o LiveCycle Designer pesquisa o formulário por Texto personalizado, Dica de ferramenta, Legenda e Propriedades de nome, nessa ordem, para encontrar o texto a ser lido por leitores de tela. Você pode substituir essa ordem padrão usando a opção Precedência de Reader da tela na paleta Acessibilidade:

1. Selecione o objeto no design do formulário.
1. Clique na paleta Acessibilidade.
1. Selecione qualquer opção de Precedência de Reader da tela diferente de Nenhum.

As opções disponíveis são as seguintes:

* **Texto personalizado**, que você define no campo Texto de Reader da tela personalizada da paleta de acessibilidade. Essa opção permite especificar qualquer texto que você deseja que a tecnologia assistiva, como leitores de tela, use. O uso da configuração de Legenda é melhor para a maioria das situações. Criar texto de Reader de tela personalizada deve ser considerado uma opção somente quando a Legenda ou uma dica de ferramenta não forem possíveis.
* **Dica de Ferramenta**, que você definiu no campo Dica de Ferramenta da paleta Acessibilidade. Para a maioria dos objetos, as dicas de ferramentas aparecem em tempo de execução quando o usuário passa o ponteiro do mouse sobre o objeto. As dicas de ferramenta são exibidas para alguns objetos somente leitura, como o objeto de código de barras de um formulário de papel, somente quando um leitor de tela está em uso.
* **Legenda**, que fará com que o LiveCycle Designer use o rótulo associado (visual) do campo de formulário como texto de leitor de tela.
* **Nome**, que você definiu no campo Nome da guia Associação. Observe que esse nome não pode conter espaços.
* **Nenhum**, o que fará com que o objeto não tenha um nome. Isso nunca é recomendado para controles de formulário.

Considere o seguinte ao usar a paleta Acessibilidade para rotulagem de controle de formulário:

* Se a legenda do controle de formulário descrever o controle corretamente, ele poderá ser acessado por leitores de tela. Nesse caso, deixe os campos Texto personalizado e Dica de ferramenta vazios na paleta Acessibilidade ou altere a Precedência de Reader da tela para Legenda.
* Ao direcionar leitores de tela, não adianta especificar descrições de texto diferentes para o mesmo controle de formulário, pois somente uma será usada: o primeiro campo não vazio na ordem de Precedência de Reader da tela. Por exemplo, não há motivo para especificar Texto personalizado e Texto de dica de ferramenta para um leitor de tela.
* Por padrão, o leitor de tela lê a legenda se nada for especificado na caixa Dica de ferramenta ou Texto de Reader de tela personalizado.
* Não use a paleta Acessibilidade para criar descrições de campos ou áreas invisíveis.
* Se você precisar criar uma descrição usando as opções de Dica de ferramenta ou Texto de Reader de tela personalizado, sempre inclua a legenda que está visível no formulário, exceto quando a legenda visível não for significativa, por exemplo, quando a própria legenda estiver abreviada. Isso ajuda os usuários de leitores de tela a se comunicarem de maneira eficaz com outros usuários sobre os elementos da interface do usuário. Esses diferentes grupos de usuários têm dificuldade em identificar o mesmo elemento da interface do usuário se o texto da legenda for diferente da Dica de ferramenta ou do Texto de Reader da tela personalizada.
* Para caixas de seleção e controles de lista suspensa em células de tabela, o leitor de tela anunciará qualquer legenda, dica de ferramenta ou texto personalizado de leitor de tela especificado para o objeto. Se quiser usar o cabeçalho da coluna como o texto alternativo para esses objetos quando colocados em uma tabela, não forneça uma legenda, dica de ferramenta ou texto de leitor de tela personalizado.
* Se o controle exigir instruções adicionais, verifique se elas também estão incluídas na alternativa em texto. Inclua informações faladas suficientes para que os usuários saibam qual entrada é esperada e como preencher o campo corretamente, mas não sobrecarregue os usuários com informações redundantes.
* Não forneça informações desnecessárias descrevendo como operar controles - permita que as tecnologias assistivas do usuário lidem com isso para o usuário. Os usuários podem configurar a verbosidade para se adequar aos seus níveis de conforto.

A Figura 4 mostra um exemplo de um campo de texto com uma legenda visual que pode não estar clara para alguns usuários de leitores de tela. Neste exemplo, o Texto de Reader da tela personalizada está definido como &quot;Número de páginas&quot; e a Precedência de Reader da tela está definida como Texto personalizado. Como resultado, o texto da legenda real (visual) (&quot;# de páginas&quot;) não será usado pelo leitor de tela. Como alternativa, uma Dica de ferramenta pode ter sido especificada.

![Especificando o Texto de Reader de Tela Personalizada quando o rótulo visível é inadequado](/help/forms/using/assets/image-4.png)

Figura 4: **Especificando o Texto de Reader da Tela Personalizada quando o rótulo visível for inadequado**

### Botões de opção de rotulagem

Quando um usuário com deficiência visual é inserido em um botão de opção, o leitor de tela precisa ler duas coisas:
* Uma indicação da finalidade do grupo de botões de opção
* Um rótulo significativo para cada botão de opção
Para tornar os botões de opção acessíveis usando as legendas de botão:
   1. Na paleta Hierarquia, selecione o grupo de exclusão.
   1. Clique na paleta Acessibilidade e, na caixa Texto de Reader da tela personalizada, digite o texto a ser lido para o grupo. Por exemplo, para um grupo de exclusão que indica opções de pagamento por vários cartões de crédito, digite Selecione um método de pagamento.
   1. Se as legendas de cada botão de opção fornecerem texto que será significativo quando falado por um leitor de tela, na paleta Objeto, selecione a guia Ligação e desmarque Especificar valor do item.

  Para tornar os botões de opção acessíveis usando um valor de item especificado:
   1. Na paleta Hierarquia, selecione o grupo de exclusão.
   1. Clique na paleta Acessibilidade e, na caixa Texto de Reader da tela personalizada, digite o texto a ser lido para o grupo. Por exemplo, para um grupo de exclusão que indica opções de pagamento por vários cartões de crédito, digite Selecione um método de pagamento.
   1. Na paleta Hierarquia, selecione o primeiro botão de opção no grupo.
   1. Na paleta Objeto, clique na guia Campo. Na área Item, clique duas vezes no item e digite um valor significativo para o botão de opção selecionado. Por exemplo, para o primeiro botão em um grupo de métodos de pagamento, você pode digitar Caixa.
   1. Repita as etapas 3 e 4 para cada botão de opção no grupo de exclusão.

### Rotulagem de controles personalizados

É altamente recomendável usar componentes padrão em vez de componentes personalizados, pois eles fornecerão à tecnologia assistiva as dicas e informações corretas por padrão. No entanto, se os controles personalizados forem usados, considere o seguinte:
* Anuncie o estado das caixas de seleção e botões de opção.
* Nas caixas de listagem e listas suspensas, anuncie o item padrão selecionado na lista. Certifique-se de que o usuário saiba como usar as teclas de Seta para cima e Seta para baixo para percorrer os itens da lista. Observe que pressionar a tecla Tab ou Enter ou Return selecionará o item na lista. Usando scripts, você pode definir o evento Alterar do objeto para anunciar qual item está selecionado na lista.
* Anuncie aos usuários todos os pressionamentos de tecla especiais necessários para executar uma função, por exemplo, pressionar a barra de espaço para selecionar um botão ou a tecla de seta para baixo para selecionar um item de uma caixa de listagem.

### Posicionamento correto da legenda de um controle

A colocação de uma legenda é importante porque os usuários esperam que ela seja localizada próxima ao controle. Para usuários de ampliação de tela, isso é ainda mais importante, pois talvez eles não consigam visualizar o controle e a legenda ao mesmo tempo se estiverem muito distantes um do outro.

Ao criar um objeto, o LiveCycle Designer posiciona automaticamente a legenda conforme especificado pelo tipo de objeto. As legendas de botões de opção, por exemplo, são colocadas à direita. Essa disposição padrão é sempre a melhor localização para uma legenda acessível. Se precisar alterar a posição do texto da legenda, use estas etapas:
1. Selecione o objeto movendo o foco para ele.
1. Na paleta Layout, selecione a posição da legenda do objeto na opção Posição na seção Legenda, na parte inferior da paleta.

O exemplo na Figura 5 mostra uma caixa de texto com uma legenda acima dela. A Posição na paleta Layout é definida como Superior. O local padrão da legenda é à esquerda da caixa de texto.

![Alterando o posicionamento da legenda usando a paleta Layout](/help/forms/using/assets/image-5.png)

Figura 5: **Alterando o posicionamento da legenda usando a paleta Layout**

A tabela a seguir fornece uma visão geral das regras de posicionamento de rótulo para controles usados com frequência.

| Tipo de controle | Regras de posicionamento |
|--------------|-----------------|
| Entrada de texto (incluindo campos de data, hora e senha) | Coloque a legenda à esquerda do controle (padrão). Se isso não for possível, coloque-o imediatamente acima ou abaixo dele. Os rótulos devem ser posicionados perto do controle para usuários com ampliação aumentada, de modo que o rótulo e o controle tenham maior probabilidade de serem vistos juntos na exibição ampliada. |
| Caixa de seleção | Coloque a legenda à direita da caixa de seleção (padrão). Para controles de caixa de seleção em células de tabela, o leitor de tela anunciará qualquer legenda, dica de ferramenta ou texto de leitor de tela personalizado que você especificar para o objeto. Se quiser usar o cabeçalho da coluna como texto alternativo para uma caixa de seleção em uma tabela, não forneça uma legenda, dica de ferramenta ou texto de leitor de tela personalizado. |
| Grupo de botões de opção | Crie um título visível para o grupo de botões de opção criando um elemento de texto estático e colocando-o à esquerda ou acima do grupo. Para cada botão de opção individual, coloque o rótulo à direita (padrão). |
| Lista suspensa | Coloque a legenda à esquerda do objeto (padrão). Se isso não for possível, coloque-o imediatamente acima dele. Para controles de lista suspensa em células de tabela, o leitor de tela anunciará qualquer legenda, dica de ferramenta ou texto de leitor de tela personalizado que você especificar para o objeto. Se quiser usar o cabeçalho da coluna como texto alternativo para esses objetos em uma tabela, não forneça uma legenda, dica de ferramenta ou texto de leitor de tela personalizado. |
| Caixa de listagem | A legenda é posicionada acima da caixa de listagem por padrão ao criá-la. |
| Botão | A legenda é colocada automaticamente no botão e não precisa ser posicionada manualmente. Verifique se a finalidade do botão está descrita corretamente pelo texto da legenda. |


### Preencher dinamicamente uma dica de ferramenta ou um texto de Reader de tela personalizado

Também é possível preencher dinamicamente uma alternativa de texto do controle de formulário, como a Dica de ferramenta, com um valor de uma fonte de dados. Por exemplo, você pode exibir uma Dica de ferramenta personalizada para um objeto em francês.
O esquema ao qual você se conecta pode ter o seguinte definido para uma Dica de ferramenta:


```html
<form>
<tooltip dp_tt="tooltip1"/>
</form>
```


O arquivo de dados para o qual você aponta pode ter o seguinte definido para uma dica de ferramenta:

```html
<form>
<tooltip dp_tt="Quantité - Entrez un nombre inférieur ou égal à 100."/>
</form>
```

1. Na paleta Biblioteca de objetos, clique na categoria Padrão e arraste um objeto para o design do formulário. Por exemplo, insira um objeto Campo de texto.
1. (Opcional) Na paleta Objeto, clique na guia Campo e digite uma legenda para o objeto na caixa Legenda. Por exemplo, digite Quantité.
1. Na paleta Acessibilidade, clique no rótulo ativo Dica de ferramenta.
1. Selecione a conexão de dados.
1. Clique no triângulo ao lado da caixa Associação e selecione uma associação. Por exemplo, selecione dica de ferramenta > @dp_tt.

A seguinte string aparece na caixa Vinculação: $record.tooltip.dp_tt Dica: você poderia digitar essa string na caixa Itens em vez de selecioná-la.
1. Clique em OK.
1. Exiba o formulário na guia Preview PDF.

### Fornecimento do texto do link

Os usuários de tecnologia assistiva podem ter diferentes métodos de leitura do texto vinculado. Por exemplo, os usuários de leitores de tela geralmente usam uma lista de links como a mostrada na Figura 6 para verificar rapidamente os links disponíveis em uma página.

![Caixa de diálogo Lista de Links JAWS](/help/forms/using/assets/image-6.png)

Figura 6: **Caixa de diálogo Lista de Links JAWS**

Por essa razão, os links devem ser de autodescrição; esse é o significado deles não deve depender do contexto (o texto ao redor). Por exemplo, as palavras &quot;clique aqui&quot; podem formar o elemento de link real na frase &quot;clique aqui para baixar nosso formulário de aplicativo&quot;. Esse link seria difícil de entender ao ser lido em uma lista de links, especialmente quando há vários links contendo o mesmo texto.

Ao usar links no seu formulário, verifique se cada link descreve corretamente sua finalidade, sem depender do texto ao redor ou da posição na página. Por exemplo, em vez de usar uma frase como &quot;Clique aqui&quot; como texto do link, use &quot;Baixar formulário de aplicativo&quot; como texto do link.

**Pontos de verificação relacionados**

* Seção 508 §1194.21
   * d) As tecnologias de assistência devem dispor de informações suficientes sobre um elemento da interface do utilizador, incluindo a identidade, o funcionamento e o estado do elemento. Quando uma imagem representa um elemento de programa, as informações transmitidas pela imagem também devem estar disponíveis no texto.
   * l) Quando forem utilizados formulários eletrônicos, o formulário deve permitir que as pessoas que utilizam a tecnologia assistiva tenham acesso às informações, aos elementos de campo e à funcionalidade necessários para o preenchimento e envio do formulário, incluindo todas as direções e indicações.
* Seção 508 §1194.22
   * n) Quando os formulários eletrônicos são concebidos para serem preenchidos em linha, o formulário deve permitir que as pessoas que utilizam a tecnologia de assistência acedam às informações, aos elementos de campo e à funcionalidade necessários para o preenchimento e envio do formulário, incluindo todas as direções e indicações.
* WCAG 1.0
   * 12.4 Associe rótulos explicitamente com seus controles (P2).
   * 13.1 Identifique claramente o destino de cada link (P2).
* WCAG 2.0
   * 1.1.1 Conteúdo não textual: todo o conteúdo não textual que é apresentado ao usuário tem uma alternativa em texto que serve um propósito equivalente, exceto para as situações listadas abaixo. (Nível A)
   * 2.4.6 Títulos e rótulos: os títulos e rótulos descrevem o tópico ou o propósito. (Nível AA)
   * 3.2.4 Identificação consistente: os componentes com a mesma funcionalidade em um conjunto de páginas da Web são identificados consistentemente. (Nível AA)
   * 3.3.2 Rótulos ou instruções: os rótulos ou instruções são fornecidos quando o conteúdo requer a entrada do usuário. (Nível A)
   * 4.1.2 Nome, função, valor: para todos os componentes da interface do usuário (incluindo, mas não limitados a: elementos de formulário, links e componentes gerados por scripts), o nome e a função podem ser determinados de forma programática; estados, propriedades e valores que podem ser definidos pelo usuário podem ser definidos de forma programática; e a notificação de alterações nesses itens está disponível aos agentes do usuário, incluindo tecnologias assistivas. (Nível A)


## Verifique se a leitura e a ordem das guias estão corretas {#ensure-reading-tab-order}

É muito importante garantir uma ordem de leitura significativa ao projetar formulários acessíveis a usuários portadores de deficiências visuais ou outras deficiências. Normalmente, esses usuários não usam o mouse para navegar em um formulário, portanto, eles dependem do teclado. A ordem de leitura determina a sequência usada pelos usuários de leitores de tela à medida que leem o formulário. Além disso, a ordem de tabulação permite que os usuários movam rapidamente de um controle de formulário interativo para o próximo usando as teclas Tab ou Shift+Tab. Uma ordem de guias lógica garante que eles tenham acesso a todos os campos no formulário e que possam navegar pelo formulário de uma forma sensata e eficiente.

A ordem de leitura do formulário inclui todos os objetos estáticos (como texto e imagens) e objetos de campo, mas somente os controles de formulário interativos fazem parte da ordem de tabulação.

>[!NOTE]
> Em muitos casos, a ordem de tabulação está intimamente relacionada à ordem de leitura. Para simplificar, o termo &quot;ordem de tabulação&quot; será usado no lugar de &quot;ordem de tabulação ou leitura&quot; neste guia.

### A ordem de tabulação padrão nos formulários do LiveCycle Designer

A ordem de tabulação padrão é criada automaticamente quando você salva o formulário como um PDF marcado. Inicialmente, a ordem de tabulação em um formulário é determinada a partir da posição local dos objetos usando as seguintes regras:

* Todos os objetos são ordenados da esquerda para a direita e de cima para baixo (ordem local), começando pelo canto superior esquerdo do formulário.
* Quaisquer subformulários criados são tratados como unidades independentes e também são navegados da esquerda para a direita e de cima para baixo. Se dois subformulários estiverem posicionados um ao lado do outro e ambos contiverem objetos, a ordem de leitura navegará por todos os objetos no primeiro subformulário antes de passar para o próximo subformulário.

Para formulários simples (ou seja, formulários com layout da esquerda para a direita, de cima para baixo), a ordem de tabulação padrão geralmente estará correta. Para verificar isso, examine a ordem de guias padrão antes de publicar o formulário. Você pode tornar a ordem das guias visível usando um dos seguintes métodos:

* Escolha Exibir > Mostrar ordem de tabulação.
* Clique em Mostrar ordem na paleta Ordem da guia.

Todos os objetos serão exibidos com um número no canto superior direito, indicando o local do objeto na ordem de tabulação padrão. Os objetos interativos nesta sequência formam a ordem de tabulação. A Figura 7 mostra a visualização da ordem de leitura de um formulário básico.

![Visualização da ordem de leitura padrão para um formulário de pedido típico](/help/forms/using/assets/image-7.png)

Figura 7: **Visualização da ordem de leitura padrão para um formulário de pedido típico**

Cada número de ordem de tabulação é mostrado em uma forma colorida. As formas têm o seguinte significado:
* Círculos cinza (#1 e #4) são usados para objetos na área de conteúdo.
* Círculos verdes (#6 e #7) são usados para objetos de página-mestre.
* Quadrados alfazejados (#2 e #3) são usados para objetos dentro de um fragmento.

Você pode optar por mostrar apenas controles de formulário interativos (que compõem a ordem de tabulação) ou todos os objetos na ordem de leitura (que também inclui objetos estáticos, como texto e imagens). Para alterar essa preferência, escolha Ferramentas > Opções > Ordem de tabulação e selecione Somente mostrar ordem de tabulação para campos.

Em um formulário complexo, pode ser difícil ver como a tabulação flui de um objeto para o próximo. Você pode usar auxílios visuais para ajudar a ver o fluxo de tabulação no formulário. Com as ajudas visuais ativadas, ao passar o ponteiro sobre o objeto, setas azuis mostram o fluxo de tabulação para os dois objetos anteriores e dois seguintes na ordem de tabulação (veja a Figura 8).

![As ajudas visuais realçam a ordem das guias](/help/forms/using/assets/image-8.png)

Figura 8: **Ajudas visuais para realçar a ordem das guias**

Para ativar as ajudas visuais, use os seguintes métodos:
* Escolha Ferramentas > Opções > Ordem de tabulação e, no painel Ordem de tabulação, selecione Exibir ajudas visuais adicionais para a ordem de tabulação.
* No menu da paleta Ordem de tabulação, selecione Mostrar ajudas visuais.

### Usar a posição para influenciar a ordem de tabulação padrão

Para influenciar a ordem de tabulação padrão, é possível alterar as coordenadas de um objeto movendo-o para um local diferente. Por exemplo, na Figura 9, o campo Nome do produto ocorre na ordem de tabulação antes do campo Quantidade. Para alterar esse pedido, você pode mover o campo Nome do produto para que ele seja colocado abaixo ou à direita do campo Quantidade.

![A ordem de tabulação padrão é da esquerda para a direita](/help/forms/using/assets/image-9.png)

Figura 9: **A ordem de tabulação padrão é da esquerda para a direita**

Você pode alterar a posição de um objeto seguindo um destes procedimentos:
* Arraste-o usando o mouse
* Selecione-o e mova-o usando as teclas de seta do teclado.

>[!NOTE]
> Pode ser útil manter o alinhamento do objeto escolhendo Exibir > Ajustar à grade.

Você pode alterar as coordenadas de um objeto com mais precisão usando a paleta Layout (mostrada na Figura 10). Essa paleta permite especificar as coordenadas X e Y, bem como a largura e a altura do objeto.

![Usando coordenadas para posicionar um objeto com precisão com a paleta Layout](/help/forms/using/assets/image-10.png)

Figura 10: **Uso de coordenadas para posicionar com precisão um objeto com a paleta Layout**

>[!NOTE]
> Quando a legenda e o controle não são mesclados, a posição da legenda de um controle de formulário é independente da ordem em que os leitores de tela leem o objeto e seus elementos. Para obter mais informações sobre legendas, consulte a seção 2.5 Fornecer rótulos adequados para controles de formulário neste guia.

### Uso de subformulários para influenciar a ordem de tabulação padrão

Como mencionado acima, os subformulários permitem inserir grupos de objetos que têm sua própria ordem de tabulação. Você pode criar um subformulário seguindo um destes procedimentos:
* Escolha Inserir > Padrão > Subformulário.
* Selecione os objetos na paleta Hierarquia e agrupe-os em um subformulário escolhendo Inserir > Quebrar no Subformulário.
* Selecione os objetos no formulário real, clique com o botão direito do mouse na seleção e escolha Quebrar no Subformulário

Quando dois subformulários contendo objetos de campo são posicionados lado a lado, a sequência de tabulação passa pelos campos no primeiro subformulário antes de passar para o próximo. Isso é ilustrado na Figura 11, onde dois subformulários são usados para criar uma ordem de tabulação padrão baseada em colunas.

![Ordem de tabulação padrão usando subformulários](/help/forms/using/assets/image-11.png)

Figura 11: **Ordem de tabulação padrão usando subformulários**

Subformulários, botões de opção e áreas de conteúdo, juntamente com a posição vertical dos objetos em uma página e sua página-mestre, afetam a ordem de tabulação.

### Criação de uma ordem de tabulação personalizada usando a paleta Ordem de tabulação

Você pode alterar a ordem de tabulação padrão quando precisar de uma sequência diferente no formulário e a alteração não puder ser obtida com o posicionamento ou agrupamento em subformulários. Para alterar a ordem de tabulação padrão, é possível criar uma ordem de tabulação personalizada usando a paleta Ordem de tabulação.
A paleta Ordem de tabulação (veja a Figura 12) permite inspecionar e modificar a ordem em que os objetos no seu formulário são lidos pela tecnologia assistiva e navegados pela tecla Tab do usuário.

![A paleta Ordem de Tabulação](/help/forms/using/assets/image-12.png)

Figura 12: **A paleta Ordem de Tabulação**

A paleta Ordem de tabulação fornece uma visualização alternativa da ordem de tabulação no formulário. Ele mostra todos os objetos no formulário como uma lista numerada, onde cada número representa a posição do objeto no fluxo de tabulação.
Para abrir a paleta Ordem de tabulação, escolha Janela > Ordem de tabulação.


A paleta Ordem de tabulação fornece os seguintes marcadores visuais:
* Uma barra cinza marca cada página do formulário. A ordem de tabulação em cada página começa com o número 1.
* A letra M dentro de um círculo verde indica objetos da página-mestre (visíveis somente ao exibir o formulário na guia Design View).
* Um intervalo de números indica objetos dentro de um fragmento.
* Um fundo amarelo indica o item selecionado no momento.
* Um ícone de bloqueio ao lado do primeiro objeto na página indica que o objeto não pode ser movido dentro da ordem de tabulação (visível somente ao visualizar o formulário na guia Páginas Mestras).

A lista mostra os mesmos números de ordem de tabulação que os números exibidos no próprio formulário quando você escolhe Exibir > Mostrar ordem de tabulação. Você altera a posição de um objeto na ordem de tabulação movendo o objeto para cima ou para baixo na lista da paleta Ordem de tabulação. Você pode mover um único objeto ou um grupo de objetos. Isso pode ser feito por meio de um dos seguintes métodos:

* Arraste o objeto selecionado para cima ou para baixo na lista e coloque-o no local desejado. Uma alça preta marca sua posição atual na lista antes de você colocar o objeto.
* Na paleta Ordem de tabulação, clique nos botões de seta para cima ou para baixo até que o objeto selecionado seja colocado na posição correta. Como alternativa, pressione Ctrl+Seta para cima ou Ctrl+Seta para baixo.
* No menu da paleta Ordem de tabulação, selecione Mover para cima ou Mover para baixo.
* Na lista da paleta Ordem de tabulação, clique no objeto selecionado (ou selecione-o e pressione F2) para tornar editável o número listado ao lado do nome do objeto. Em seguida, digite o número que indica a nova posição do objeto na ordem de tabulação e pressione Enter.
* Selecione Copiar no menu da paleta Ordem de tabulação e, na lista, selecione o objeto acima do qual deseja colocar o objeto que está sendo movido e selecione Colar no menu.

Quando você move o objeto para um novo local na ordem, o LiveCycle Designer reatribui os números da ordem de tabulação. Embora a ordem de tabulação dos objetos localizados em uma página-mestre seja exibida na guia Visualização de Design, é possível alterar a ordem desses objetos somente na guia Páginas-Mestre. Se você usar referências de fragmento no formulário, a ordem das guias dentro de um fragmento ficará visível ao visualizar a ordem do formulário. Para alterar a ordem de tabulação dentro de um fragmento, é necessário abrir o arquivo de origem do fragmento para edição, fazer a alteração e salvar o arquivo. Quaisquer formulários que usam esse fragmento são afetados por essa alteração.

Se você decidir que não deseja a ordem de tabulação personalizada no formulário, poderá retornar rapidamente para a ordem de tabulação automática (padrão) usando as seguintes etapas (você perderá todas as alterações feitas na ordem de tabulação):
1. Na paleta Ordem de tabulação, selecione Automático.
1. Na caixa de mensagem exibida, clique em Sim para confirmar a remoção da ordem de tabulação personalizada.

**Pontos de verificação relacionados**
* Seção 508 §1194.21
   * a) Quando osoftwareé concebido para funcionar num sistema que tem um teclado, as funções do produto devem ser executáveis a partir de um teclado, onde a própria função ou o resultado da execução de uma função possam ser discernidos textualmente.
* WCAG 1.0
   * 9.2 Certifique-se de que qualquer elemento que tenha sua própria interface possa ser operado de maneira independente de dispositivos.
* WCAG 2.0
   * 1.3.2 Sequência significativa: quando a sequência na qual o conteúdo é apresentado afeta seu significado, uma sequência de leitura correta pode ser determinada programaticamente. (Nível A)
   * 2.1.1 Teclado: todas as funcionalidades do conteúdo são operáveis por meio de uma interface de teclado sem exigir tempos específicos para pressionamentos de teclas individuais, exceto quando a função subjacente requer uma entrada que depende do caminho do movimento do usuário, não apenas dos pontos finais. (Nível A)
   * 2.1.3 Teclado (sem exceção): toda a funcionalidade do conteúdo é operável por meio de uma interface de teclado, sem exigir tempos específicos para pressionamentos de teclas individuais. (Nível AAA)
   * 2.4.3 Ordem de foco: se uma página da Web puder ser navegada sequencialmente e as sequências de navegação afetarem o significado ou a operação, os componentes focalizáveis receberão foco em uma ordem que preserve o significado e a operabilidade. (Nível A)


## Garantir que os controles de formulário estejam acessíveis ao teclado{#ensure-keyboard-accessible}

Os usuários devem ser capazes de preencher completamente o formulário usando apenas o teclado ou um dispositivo de entrada alternativo equivalente. Os usuários com mobilidade reduzida ou visão prejudicada podem não ter outra escolha a não ser usar o teclado, e muitos usuários que podem usar um mouse simplesmente preferem a entrada do teclado. Ao permitir vários métodos de entrada, você não apenas cria formulários acessíveis, mas também cria formulários mais adequados às preferências de todos os usuários.

No LiveCycle Designer, a maneira mais fácil de garantir que seus controles estejam acessíveis ao teclado é usando os controles listados na guia Comum da paleta Biblioteca de objetos. Esses controles respondem à entrada do mouse e do teclado por padrão. Para obter mais informações, consulte a seção 2.3 Escolha os controles corretos neste guia.

Outro aspecto importante da acessibilidade do teclado é garantir que cada elemento interativo faça parte da ordem de tabulação do formulário. Isso permite que o usuário mova o cursor para frente e para trás pelo formulário com as teclas Tab e Shift+Tab. Certifique-se de definir uma ordem lógica de tabulação que inclua todos os campos e botões. Para obter mais informações, consulte a seção 2.6. Verifique se a leitura e a ordem das guias estão corretas neste guia.

Por fim, é importante garantir que o comportamento com script também seja acessível pelo teclado e não dependa de eventos específicos do dispositivo. O evento MouseEnter do mouse, por exemplo, não pode ser executado com o teclado. Além disso, esses manipuladores de eventos não devem interferir na acessibilidade do teclado. Por exemplo, verifique se os eventos Change usados em listas suspensas ou caixas de listagem não acionam ações inesperadas.

**Pontos de verificação relacionados**
* Seção 508 §1194.21
   * a) Quando osoftwareé concebido para funcionar num sistema que tem um teclado, as funções do produto devem ser executáveis a partir de um teclado, onde a própria função ou o resultado da execução de uma função possam ser discernidos textualmente.
* WCAG 1.0
   * 6.4 Para scripts e applets, verifique se os manipuladores de eventos são independentes de dispositivos de entrada (P2).
   * 9.2 Certifique-se de que qualquer elemento que tenha sua própria interface possa ser operado de maneira independente de dispositivo (P2).
   * 9.3 Para scripts, especifique manipuladores de eventos lógicos em vez de manipuladores de eventos dependentes de dispositivo (P2).
* WCAG 2.0
   * 2.1.1 Teclado: todas as funcionalidades do conteúdo são operáveis por meio de uma interface de teclado sem exigir tempos específicos para pressionamentos de teclas individuais, exceto quando a função subjacente requer uma entrada que depende do caminho do movimento do usuário, não apenas dos pontos finais. (Nível A)
   * 2.1.2 Nenhuma armadilha de teclado: se o foco do teclado puder ser movido para um componente da página usando uma interface do teclado, o foco poderá ser movido para fora desse componente usando apenas uma interface de teclado e, se for necessário mais do que teclas de seta ou tabulação não modificadas ou outros métodos de saída padrão, o usuário será avisado do método para afastar o foco. (Nível A)
   * 2.1.3 Teclado (sem exceção): toda a funcionalidade do conteúdo é operável por meio de uma interface de teclado, sem exigir tempos específicos para pressionamentos de teclas individuais. (Nível AAA)


## Usar a cor com responsabilidade{#use-color-responsibly}

A criação de formulários para acessibilidade envolve a consideração de algumas diretrizes adicionais para o uso de cores. Os designers usam cores para melhorar a aparência dos formulários destacando vários componentes de formulário. O uso inadequado de cores, no entanto, pode dificultar ou impossibilitar a leitura de informações em sua forma por pessoas com deficiência.

### Não transmitir informações usando apenas cores

As cores podem realçar e aprimorar determinadas partes do formulário, mas você não deve transmitir informações somente por cor.

Qualquer informação transmitida exclusivamente em cores (cores com significado semântico) não é acessível a usuários cegos. O mesmo se aplica a usuários com deficiências de visão de cores ou usuários que usam esquemas de cores diferentes, como uma tela de cores de alto contraste com texto branco ou primeiro plano em um plano de fundo preto. Você também deve ter em mente que os leitores de tela não podem detectar informações de cores automaticamente.

Por exemplo, a Figura 13 mostra um campo de formulário que tem uma legenda vermelha (especificada usando a paleta Fonte) para indicar que o campo de formulário é obrigatório. Neste exemplo, a cor é o único significante da diferença entre campos de entrada obrigatórios e opcionais, o que torna impossível para usuários cegos ou usuários com determinados tipos de cegueira de cores diferenciá-los.

![Usando somente a cor para transmitir informações](/help/forms/using/assets/image-13.png)

Figura 13: **Usando somente cor para transmitir informações**

Para resolver esse problema, indique também o status obrigatório do formulário no texto alternativo do controle de formulário (conforme descrito na seção 2.5. Forneça rótulos adequados para controles de formulário). Por exemplo, você pode definir o texto do leitor de tela como &quot;Zip code (obrigatório)&quot;. Para usuários que têm dificuldades em ver a cor em determinadas combinações, é recomendável definir o tipo de campo de texto como Informado pelo usuário - Obrigatório na paleta Objeto, além de texto alternativo que indica que o campo é obrigatório. Como alternativa, você pode usar outras indicações além da cor, como texto visual, estilos de texto e estilos de borda. No entanto, para usuários de leitores de tela, ainda será necessário transmitir as informações necessárias usando a paleta Acessibilidade.

Além disso, ao fornecer descrições ou instruções ao usuário do formulário, lembre-se de que as declarações baseadas apenas em cores são insuficientes para usuários com deficiência visual. Por exemplo, em vez de uma instrução como &quot;Clique no botão verde para continuar&quot;, use uma descrição de texto para ações, como &quot;Clique no botão Avançar para continuar&quot;.

>[!NOTE]
> Esta prática recomendada não proíbe o uso de cores. Proíbe a utilização da cor como único meio de transmissão de informações importantes. Se uma indicação visual ainda for desejada para esse tipo de informação, o designer poderá usar um asterisco ou indicador visual semelhante para marcar os campos obrigatórios.

### Fornecer contraste de cores suficiente

Muitos usuários com deficiência visual dependem do alto contraste entre o texto e o plano de fundo para ler formulários. Quando o contraste entre o plano de fundo e as cores do primeiro plano não é suficiente, um formulário pode se tornar difícil, se não impossível, de ser lido para alguns usuários. A Figura 14 mostra um exemplo de formulário com contraste insuficiente.

![Um formulário com contraste de cor insuficiente](/help/forms/using/assets/image-14.png)

Figura 14: **Formulário com contraste de cor insuficiente**

É altamente recomendável usar a fonte padrão e as cores do plano de fundo: preto em um plano de fundo branco. Se você precisar alterar essas cores padrão, escolha uma combinação apropriada de cores de alto contraste; use uma cor de primeiro plano escura em uma cor de plano de fundo clara ou vice-versa. Para ter certeza, use uma ferramenta (como o Analisador de contraste de cor WAT-C) para verificar se o contraste é suficiente.

O Adobe Reader e o Adobe Acrobat permitem que os usuários especifiquem se as cores precisam ser substituídas para atender às suas necessidades visuais. Os usuários podem especificar seu próprio esquema de contraste ou podem optar por usar um esquema fornecido pelo sistema operacional. Além disso, a Adobe Reader e a Adobe Acrobat têm seu próprio esquema de alto contraste que pode estar ativado. Para que essas opções sejam bem-sucedidas, a melhor abordagem é sempre usar as cores padrão.

Ao projetar o formulário, teste-o frequentemente usando uma configuração de esquema de cores semelhante à que muitos usuários com deficiências visuais usarão para preencher o formulário. Esta prática ajuda você a descobrir e corrigir problemas no início do processo de design.

Recommendations para usar cores:
* Certifique-se de que nenhuma informação seja perdida se a cor semântica não estiver visível.
* Se não for possível usar cores padrão, verifique se suas cores têm alto contraste, como preto em um fundo claro (branco). Os usuários com deficiências visuais geralmente exigem um alto contraste entre o texto e seu plano de fundo para serem capazes de lê-lo.
* Teste a legibilidade dos formulários alternando a tela para uma exibição de alto contraste, no Windows e no Adobe Reader ou Adobe Acrobat. O Mac OSX oferece apenas um filtro de tons de cinza simples para contraste alto, portanto, isso não é suficiente para testes.
* Não transmita informações exclusivamente com base na cor. Por exemplo, não use apenas cores para realçar partes importantes do texto. Use outros métodos de realce e descrições de texto também.
* Não use muitas cores, pois isso pode dificultar a leitura das informações reais no conteúdo. Sempre mantenha a legibilidade das informações como sua prioridade principal ao decidir quais cores usar.

**Pontos de verificação relacionados**
* Seção 508 §1194.21
   * i) A codificação por cores não deve ser utilizada como único meio de transmissão de informações, indicação de uma ação, solicitação de resposta ou distinção de um elemento visual.
* WCAG 1.0
   * 2.1 Verifique se todas as informações transmitidas com a cor também estão disponíveis sem cor, por exemplo, a partir do contexto ou da marcação.
   * 2.2 Verifique se as combinações de cores do primeiro plano e do plano de fundo fornecem contraste suficiente quando visualizadas por alguém com déficits de cores ou quando visualizadas em uma tela preta e branca. [Prioridade 2 para imagens, Prioridade 3 para texto] (P2).
* WCAG 2.0
   * 1.4.1 Utilização de cor: a cor não é utilizada como o único meio visual de transmissão de informações, indicando uma ação, solicitando uma resposta ou distinguindo um elemento visual. (Nível A)
   * 1.4.3 Contraste (Mínimo): a apresentação visual de texto e imagens de texto tem uma taxa de contraste de pelo menos 4.5:1, exceto para o seguinte: (Nível AA)
   * 1.4.6 Contraste (Aprimorado): a apresentação visual de texto e imagens de texto tem uma relação de contraste de pelo menos 7:1, exceto para o seguinte: (Nível AAA)


## Fornecer células de cabeçalho para tabelas{#provide-heading-cells}

As tabelas são uma maneira eficaz de organizar e apresentar conteúdo em formulários acessíveis. Quando usados adequadamente, as linhas e colunas de uma tabela fornecem uma estrutura previsível e consistente para o conteúdo do formulário. Por exemplo, quando um usuário de leitor de tela navega para uma célula de linha de corpo, o leitor de tela especifica o local da célula e lê o conteúdo dela. O leitor de tela especifica o local da célula usando uma combinação de cabeçalhos de linha e coluna ou números de linha e coluna. Como os leitores de tela fornecem informações que orientam o usuário para o local do conteúdo na tabela, seu layout afeta diretamente a acessibilidade da tabela.

Você pode especificar as seguintes funções para elementos de tabela ao construir tabelas. Essas funções permitem que os leitores de tela naveguem na estrutura da tabela usando atalhos especiais e transmitirão ao usuário a relação entre as células da tabela e as células do cabeçalho correspondentes.
* Tabela
Atribui a função de uma tabela ao subformulário selecionado. Quando o usuário navega para esse subformulário, a maioria dos leitores de tela o identifica como uma tabela e indica o número de linhas e colunas.
* Linha de cabeçalho
Atribui a função de uma linha de cabeçalho ao subformulário ou linha de tabela selecionada. Ao falar o conteúdo de uma célula da linha de corpo, a maioria dos leitores de tela identifica primeiro o conteúdo da célula correspondente na linha de cabeçalho.
* Linha do corpo
Atribui a função de uma linha de corpo ao subformulário ou linha de tabela selecionada. Se uma célula contiver um subformulário, os leitores de tela normalmente falarão o conteúdo da célula correspondente na linha de cabeçalho, seguido pelos campos no subformulário.
* Linha de rodapé
Atribui a função de uma linha de rodapé ao subformulário ou linha de tabela selecionada.
* (Nenhum)
Especifica uma linha que transmite informações sobre a tabela ou seu conteúdo. A linha não é considerada parte da tabela; no entanto, o leitor de tela lerá seu conteúdo.

Quando usadas corretamente, as tabelas são uma maneira eficaz de organizar e apresentar informações tabulares. Evite tabelas muito complexas, como aquelas com tabelas e seções aninhadas.

### Como tornar tabelas simples acessíveis

Tabelas com layouts simples são recomendadas. Tabelas simples começam com uma única linha de cabeçalho seguida pelas linhas de corpo.

Ao criar tabelas simples para acessibilidade, lembre-se destas diretrizes:

* A ordem de tabulação de uma tabela é geográfica, que é a mesma do próprio formulário. Certifique-se de que o conteúdo da tabela esteja organizado de forma que faça sentido quando for lido da esquerda para a direita e de cima para baixo.
* A maioria dos leitores de tela interpreta a primeira linha de uma tabela como a linha de cabeçalho. Ao ler o conteúdo de uma célula da linha de corpo, esses leitores de tela leem primeiro o conteúdo da célula da linha de cabeçalho associada. Verifique se o conteúdo em cada célula da linha de cabeçalho descreve significativamente o conteúdo da coluna.
* Evite células que se estendem por duas ou mais colunas, tabelas aninhadas ou seções de tabela. Alguns leitores de tela têm dificuldade em interpretar esses recursos corretamente ou podem não usá-los. Por exemplo, se uma célula em uma linha de corpo abranger duas colunas, os leitores de tela talvez não façam referência ao conteúdo de célula correto na linha de cabeçalho ao ler a próxima célula na linha.

### Tornando tabelas complexas acessíveis

Ao projetar tabelas para acessibilidade, esforçar-se-á para manter o layout da tabela simples, com uma linha de cabeçalho seguida por linhas de corpo. É claro que algum conteúdo pode exigir um layout de tabela mais complexo. Por exemplo, talvez seja necessário usar a abrangência de célula ou mais de um cabeçalho para transmitir efetivamente o conteúdo.

Você pode criar tabelas complexas usando o objeto de tabela ou combinando objetos de subformulário. O objeto de tabela permite usar recursos destinados a ajudar no processo de design, como opções para inserir e redimensionar colunas e linhas.

Usando a paleta Acessibilidade, você pode especificar funções relacionadas à tabela para subformulários a fim de criar uma tabela complexa acessível. Dependendo da experiência de design e das preferências, você pode optar por criar tabelas complexas combinando objetos de subformulário. Por exemplo, você pode criar um subformulário que inclua duas linhas e especificar esse subformulário como o cabeçalho da tabela e especificar outro subformulário para as linhas de corpo da tabela.

Ao usar objetos de subformulário em vez de objetos de tabela para criar tabelas, as seguintes etapas adicionais são necessárias:
* Na guia Subformulário, defina o tipo para cada subformulário como Posicionado.
* Na paleta Acessibilidade, defina a função de subformulário apropriada para cada subformulário que compõe a tabela. Por exemplo, atribua a função de Linha de cabeçalho ao subformulário usado como o cabeçalho da tabela.
* Para linhas que transmitem informações sobre a tabela ou seu conteúdo, mas que não são consideradas parte da tabela, atribua a função de subformulário Nenhum. O leitor de tela lerá o conteúdo da linha.

Os recursos compatíveis com o leitor de tela determinam as informações lidas para uma tabela complexa. Por exemplo, considere uma tabela que inclui uma linha de cabeçalho e uma seção com uma linha de cabeçalho. Quando o usuário navega para uma célula da linha do corpo na seção da tabela, os leitores de tela normalmente leem o seguinte conteúdo, em ordem:
* Conteúdo da célula apropriada na linha de cabeçalho da tabela
* Conteúdo da célula apropriada na linha de cabeçalho da seção
* Conteúdo da célula selecionada
No entanto, alguns leitores de tela podem não ler o conteúdo de ambas as linhas de cabeçalho.

Crie nomes ou títulos visíveis significativos para suas tabelas. Você pode criar um nome de tabela como texto estático no Adobe LiveCycle Designer e colocá-lo na frente da tabela. Você pode agrupar uma tabela e seu nome em um subformulário. Os subformulários são particularmente úteis quando você deseja combinar objetos associados em um layout.

Para controles em células de tabela, o leitor de tela anunciará qualquer legenda, dica de ferramenta ou texto personalizado do leitor de tela especificado para o objeto. Se quiser usar o cabeçalho da coluna como texto alternativo para um controle em uma tabela, não forneça uma legenda, dica de ferramenta ou texto de leitor de tela personalizado. Esteja ciente, no entanto, de que essa estratégia nem sempre é tão clara para os usuários de leitores de tela, pois os leitores de tela só podem associar o cabeçalho da coluna ao controle quando o usuário não está no modo de interação de formulário do leitor de tela.

**Pontos de verificação relacionados**
* Seção 508 §1194.22
   * g) Os cabeçalhos de linhas e colunas devem ser identificados para quadros de dados.
   * h) A marcação deve ser utilizada para associar células de dados e células de cabeçalho a tabelas de dados que tenham dois ou mais níveis lógicos de cabeçalhos de linhas ou colunas.
* WCAG 1.0
   * 5.1 Para tabelas de dados, identifique cabeçalhos de linha e coluna (P1).
   * 5.2 Para tabelas de dados que tenham dois ou mais níveis lógicos de cabeçalhos de linha ou coluna, use a marcação para associar células de dados e células de cabeçalho (P1)
* WCAG 2.0
   * 1.3.1 Informações e Relações: as informações, a estrutura e as relações transmitidas por meio da apresentação podem ser determinadas programaticamente ou estão disponíveis em texto. (Nível A)


## Fornecer uma estrutura de formulário navegável{#provide-navigable-form}

Quando um formulário se torna longo e complexo, sua facilidade de uso será muito influenciada pela forma como ele é estruturado. Assim como um livro fica mais fácil de entender quando é dividido em capítulos e seções, um formulário fica mais fácil de usar quando é dividido em cabeçalhos e subtítulos. Esse particionamento é especialmente útil para usuários de leitores de tela, pelos seguintes motivos:
* Cada cabeçalho informa ao usuário do leitor de tela o que pode ser esperado na seção após o cabeçalho.
* Os leitores de tela fornecem atalhos para avançar e retroceder rapidamente entre os diferentes cabeçalhos do formulário e também permitem que o usuário acesse uma lista de cabeçalhos, que fornece uma visão geral da estrutura do documento e permite navegação rápida.

Fornecer mecanismos que permitam aos usuários pular para outras áreas do formulário pode tornar o formulário mais conveniente. É possível adicionar uma estrutura de cabeçalho ao formulário usando a paleta Acessibilidade no LiveCycle Designer.

### Fornecer mecanismos de salto

Os usuários com visão podem digitalizar uma página em qualquer ordem. Eles podem começar olhando para o canto inferior direito da página e digitalizando de volta o conteúdo. O usuário do leitor de tela não tem essa opção porque o leitor de tela começará a ler a página no canto superior esquerdo (como apresentado no código-fonte) e avançará em uma ordem linear. Além disso, o usuário com visão pode digitalizar a página em busca de links interessantes e ativá-los com o mouse. Um usuário leitor de tela deve percorrer a página sequencialmente.

A maneira mais fácil e eficaz de fornecer uma estrutura de formulário navegável é usar cabeçalhos estruturais e listas definidas corretamente no formulário.
Você também pode fornecer mecanismos que permitem que o usuário pule para outras áreas do formulário, por exemplo, adicionando botões de navegação na parte superior e inferior do formulário. Na parte superior de um formulário, você pode incluir botões como Abrir arquivo de dados, Página anterior e Próxima página. Na parte inferior do formulário, você pode incluir botões como Salvar dados, Enviar dados por email, Ir para o início da página e Imprimir.

Os campos inteligentes podem ser uma maneira eficaz de facilitar o preenchimento de alguns formulários. Por exemplo, um formulário de solicitação de viagem pode ter várias linhas e colunas de campos. Se uma linha específica estiver vazia, pressionar a tecla Tab no último item dessa linha poderá pular para a próxima seção do formulário, em vez de continuar percorrendo vários campos que permanecerão vazios.

### Adição de cabeçalhos usando a paleta Acessibilidade

Você pode usar a paleta Acessibilidade para atribuir funções a objetos com base na utilização do objeto. Essas funções podem ser aplicadas para criar cabeçalhos em diferentes níveis.

![Especificando uma função de cabeçalho na paleta de Acessibilidade](/help/forms/using/assets/image-15.png)
Figura 15: **Especificando uma função de cabeçalho na paleta de Acessibilidade**

Siga estas etapas para criar um cabeçalho no formulário:

1. Identifique o início de cada segmento lógico do formulário usando rótulos de texto estáticos,
1. Para cada rótulo e selecione uma das opções de cabeçalho como a Função na paleta Acessibilidade. Os diferentes níveis de cabeçalho (1 a 6) permitem criar uma estrutura de cabeçalho no formulário. Comece com nível 1, depois use nível 2 e assim por diante para subseções aninhadas.

A maioria dos leitores de tela permite que os usuários naveguem rapidamente entre elementos de cabeçalho com base em seus níveis. A Figura 16 mostra um formulário dividido em segmentos menores usando cabeçalhos. Neste exemplo, a seguinte estrutura de cabeçalho é usada:

* Nível do Cabeçalho 1: Solicitação de Produto
   * Nível do Cabeçalho 2: Detalhes do Pedido
      * Nível de Cabeçalho 3: Opções de Entrega
* Nível do Cabeçalho 2: Informações Adicionais
   * Nível de Cabeçalho 3: Detalhes Pessoais
   * Nível do Cabeçalho 3: Endereço

![Estruturando um formulário usando cabeçalhos](/help/forms/using/assets/image-16.png)

Figura 16: **Estruturando um formulário usando cabeçalhos**

Esses cabeçalhos são apenas elementos de texto estáticos que receberam um tamanho de fonte específico e uma função de cabeçalho com o nível apropriado.

>[!NOTE]
> Simplesmente alterar a aparência visual de um rótulo de texto para parecer um cabeçalho não fará com que os leitores de tela o reconheçam como um cabeçalho. É necessário aplicar uma função de cabeçalho.

Sempre verifique se a ordem dos níveis de cabeçalho é lógica. Por exemplo, uma subseção de um cabeçalho de nível 2 deve ser sempre um cabeçalho de nível 3; você nunca deve pular níveis ao marcar subseções. Os usuários de leitores de tela usam os diferentes níveis para obter uma melhor compreensão da estrutura do formulário. Por exemplo, depois de encontrar um cabeçalho de nível 2, o usuário pode usar um atalho para procurar cabeçalhos de nível 3 e determinar se há subseções. Se você pular os níveis, o usuário terá dificuldades em identificar essas subseções.

### Listas de marcação

Às vezes, também pode ser útil adicionar conteúdo de lista ao formulário. As listas são úteis para agrupar itens relacionados, e permitem que os usuários de leitores de tela saibam quantos itens há em uma lista e naveguem rapidamente além dela. A marcação correta de listas torna a estrutura do formulário mais clara para os usuários de leitores de tela.

No LiveCycle Designer, você cria listas usando subformulários com as seguintes etapas:

1. Selecione um subformulário que contenha o conteúdo que será marcado como itens de lista.
1. Na paleta Acessibilidade, selecione Lista como a Função.
1. Selecione cada subformulário aninhado dentro do subformulário Lista e defina sua Função como Item de lista.

>[!NOTE]
> Uma função de Item de Lista só pode ser atribuída a um subformulário contido em um subformulário que tenha uma função de Lista especificada. Você não pode definir uma tabela ou linha de tabela como uma lista ou item de lista; no entanto, um item de lista pode conter uma tabela.

**Pontos de verificação relacionados**
* Seção 508 §11934.22
   * o) Deve ser previsto um método que permita aos utilizadores pular ligações de navegação repetitivas.
* WCAG 1.0
   * 3.5 Use elementos de cabeçalho para transmitir a estrutura do documento e usá-los de acordo com a especificação (P2).
   * 3.6 Marque listas e itens de lista corretamente. (P2).
   * 12.3 Divida grandes blocos de informações em grupos mais gerenciáveis onde for natural e apropriado. (P2).
   * 13.3 Forneça informações sobre o layout geral de um site (por exemplo, um mapa do site ou índice).
   * 13.4 Use os mecanismos de navegação de maneira consistente (P2).
* WCAG 2.0
   * 1.3.2 Sequência significativa: quando a sequência na qual o conteúdo é apresentado afeta seu significado, uma sequência de leitura correta pode ser determinada programaticamente. (Nível A)
   * 2.4.1 Ignorar blocos: um mecanismo está disponível para ignorar blocos de conteúdo que são repetidos em várias páginas da Web. (Nível A)
   * 2.4.5 Várias maneiras: há mais de uma maneira disponível para localizar uma página da Web em um conjunto de páginas da Web, exceto quando a página da Web é o resultado de um processo ou uma etapa dele. (Nível AA)
   * 2.4.6 Títulos e rótulos: os títulos e rótulos descrevem o tópico ou o propósito. (Nível AA)
   * 2.4.10 Cabeçalhos de seção: os cabeçalhos de seção são usados para organizar o conteúdo. (Nível AAA)
   * 3.2.3 Navegação consistente: os mecanismos de navegação que são repetidos em várias páginas da Web em um conjunto de páginas ocorrem na mesma ordem relativa sempre que são repetidos, a menos que uma alteração seja iniciada pelo usuário. (Nível AA)


## Evitar scripts com interrupções{#avoid-disruptive-scripting}

Como parte do processo de design do formulário, os desenvolvedores de formulários podem usar scripts para fornecer uma experiência do usuário mais avançada. É possível adicionar scripts à maioria dos campos e objetos de formulário. Por exemplo, você pode criar scripts simples para atualizar dinamicamente valores em um formulário interativo em resposta à entrada do usuário.

Ao criar scripts para acessibilidade, considere estas diretrizes gerais:

* Mantenha o conteúdo do formulário livre de interrupções visuais. Por exemplo, evite recursos que façam com que o conteúdo pisque, pisque ou mova.
* Certifique-se de que as janelas pop-up sejam exibidas somente como resultado das ações iniciadas pelo usuário. Da mesma forma, não permita que o foco atual do formulário (a visualização atual do usuário) seja alterado ou que o conteúdo seja exibido novamente, a menos que seja iniciado pelo usuário. Por exemplo, se o usuário estiver preenchendo campos na metade inferior do formulário, não permita que o foco mude para o canto superior esquerdo do formulário, a menos que o usuário opte por navegar até esse local.
* Os usuários portadores de deficiências podem precisar de mais tempo para fornecer informações nos campos. Não especifique respostas com base no tempo para campos de entrada.
* Observe que os scripts do lado do cliente podem interferir nos leitores de tela e teclados se o script alterar o foco do aplicativo do cliente. Por exemplo, os eventos change e mouseEnter, quando usados com listas suspensas ou caixas de listagem, podem causar ações inesperadas. Verifique se os scripts do lado do cliente não causam problemas para usuários de leitores de tela e usuários exclusivos de teclado.
* Às vezes, os usuários de tecnologia assistiva precisarão de mais tempo para concluir as tarefas. Em qualquer caso em que uma rotina cronometrada estiver prestes a expirar, exiba uma mensagem acessível para permitir uma extensão. As caixas de alerta criadas pelo JavaScript podem ser usadas pela tecnologia assistiva. Uma nova janela com uma mensagem alertando o usuário sobre um tempo limite iminente também pode ser implantada.

**Pontos de verificação relacionados**:
* Seção 508 §1194.22
   * l) Quando as páginas utilizam linguagens de script para exibir conteúdo ou criar elementos de interface, as informações fornecidas pelo script devem ser identificadas com um texto funcional que possa ser lido por tecnologias assistivas.
   * p) Quando for necessária uma resposta cronometrada, o utilizador deve ser alertado e dispor de tempo suficiente para indicar que é necessário mais tempo.
* WCAG 1.0
   * 1.4 Para qualquer apresentação multimídia baseada em tempo (por exemplo, um filme ou uma animação), sincronize alternativas equivalentes (por exemplo, legendas ou descrições auditivas da trilha visual) com a apresentação (P1).
   * 6.2 Verifique se os equivalentes de conteúdo dinâmico são atualizados quando o conteúdo dinâmico é alterado.
   * 6.3 Certifique-se de que as páginas possam ser usadas quando scripts, applets ou outros objetos programáticos estiverem desativados ou não forem suportados. Se isso não for possível, forneça informações equivalentes em uma página alternativa acessível.
   * 6.5 Certifique-se de que o conteúdo dinâmico esteja acessível ou forneça uma apresentação ou página alternativa (P2).
   * 8.1 Torne elementos programáticos, como scripts e applets, diretamente acessíveis ou compatíveis com as tecnologias assistivas [Prioridade 1 se a funcionalidade for importante e não for apresentada em outro lugar], caso contrário (P2).
   * 9.3 Para scripts, especifique manipuladores de eventos lógicos em vez de manipuladores de eventos dependentes de dispositivo (P2).
   * 10.1 Até que os agentes do usuário permitam que os usuários desativem janelas geradas, não faça com que janelas pop-ups ou outras janelas sejam exibidas e não altere a janela atual sem informar o usuário.
* WCAG 2.0
   * 3.2.1 Em foco: quando qualquer componente recebe foco, ele não inicia uma alteração de contexto. (Nível A)
   * 3.2.2 Na entrada: alterar a configuração de qualquer componente da interface do usuário não causa uma alteração de contexto automaticamente, a menos que o usuário tenha sido avisado do comportamento antes de usar o componente. (Nível A)
   * 3.2.5 Alteração mediante solicitação: as alterações de contexto são iniciadas somente por solicitação do usuário ou um mecanismo está disponível para desativar essas alterações. (Nível AAA)

## Verifique se todo o conteúdo de áudio e vídeo está acessível{#ensure-audio-video-accessible}

Se seus formulários incorporarem conteúdo de áudio ou vídeo, incluindo clipes de áudio e vídeo, você deve garantir que esse conteúdo esteja acessível. Especificamente, verifique se os videoclipes incorporados aos formulários contêm legendas (às vezes chamadas de legendas) para usuários surdos e com deficiência auditiva e descrições de vídeo para usuários cegos. Para arquivos de áudio que não são sincronizados com o conteúdo de vídeo, uma transcrição simples é suficiente.
Para mídia baseada em Flash, consulte [link](/help/forms/using/best-practices-for-creating-forms-in-designer.md) para obter informações sobre como fornecer legendas.

**Pontos de verificação relacionados**:
* Seção 508 §1194.22
   * b) As alternativas equivalentes para qualquer apresentação multimédia devem ser sincronizadas com a apresentação.
* WCAG 1.0
   * 1.1 Forneça um equivalente em texto para cada elemento não textual (por exemplo, por meio de &quot;alt&quot;, &quot;longdesc&quot; ou no conteúdo do elemento). Isso inclui: imagens, representações gráficas de texto (incluindo símbolos), regiões de mapa de imagem, animações (por exemplo, GIF animados), applets e objetos programáticos, arte ascii, quadros, scripts, imagens usadas como marcadores de lista, espaçadores, botões gráficos, sons (reproduzidos com ou sem interação do usuário), arquivos de áudio independentes, faixas de áudio de vídeo e vídeo (P1).
   * 1.3 Até que os agentes do usuário possam ler automaticamente em voz alta o equivalente em texto de uma faixa visual, forneça uma descrição auditiva das informações importantes da faixa visual de uma apresentação multimídia (P1).
   * 1.4 Para qualquer apresentação multimídia baseada em tempo (por exemplo, um filme ou uma animação), sincronize alternativas equivalentes (por exemplo, legendas ou descrições auditivas da trilha visual) com a apresentação (P1).
* WCAG 2.0
   * 1.2.1 Apenas áudio e apenas vídeo (pré-gravado): para mídias apenas áudio e apenas vídeo pré-gravadas, os itens a seguir são verdadeiros, exceto quando o áudio ou vídeo é uma alternativa para texto e é claramente rotulado como tal: (Nível A)
   * 1.2.2 Legendas (pré-gravadas): as legendas são fornecidas para todo o conteúdo de áudio pré-gravado na mídia sincronizada, exceto quando a mídia é uma alternativa para texto e é claramente identificada como tal. (Nível A)
   * 1.2.3 Descrição de áudio ou alternativa de mídia (pré-gravada): uma alternativa para mídia com base no tempo ou descrição de áudio do conteúdo de vídeo pré-gravado é fornecida para mídia sincronizada, exceto quando a mídia é uma alternativa para texto e é claramente identificada como tal. (Nível A)
   * 1.2.4 Legendas (ao vivo): são fornecidas legendas para todo o conteúdo de áudio ao vivo na mídia sincronizada. (Nível AA)
   * Descrição de áudio 1.2.5 (pré-gravado): a descrição de áudio é fornecida para todo o conteúdo de vídeo pré-gravado na mídia sincronizada. (Nível AA)
   * 1.2.6 Linguagem de sinais (pré-gravada): a interpretação da linguagem de sinais é fornecida para todo o conteúdo de áudio pré-gravado na mídia sincronizada. (Nível AAA)
   * 1.2.7 Descrição de áudio estendido (pré-gravado): quando as pausas no áudio em primeiro plano são insuficientes para permitir que as descrições de áudio transmitam o sentido do vídeo, a descrição de áudio estendido é fornecida para todo o conteúdo de vídeo pré-gravado na mídia sincronizada. (Nível AAA)
   * 1.2.8 Alternativa de mídia (pré-gravada): uma alternativa para mídia baseada no tempo é fornecida para todas as mídias sincronizadas pré-gravadas e para todas as mídias apenas de vídeo pré-gravadas. (Nível AAA)
   * 1.2.9 Somente áudio (ao vivo): É fornecida uma alternativa para mídia baseada em tempo que apresenta informações equivalentes para conteúdo somente áudio ao vivo. (Nível AAA)

## Identificar o idioma natural e quaisquer alterações no idioma{#identify-natural-language}

O conteúdo do formulário será lido por tecnologias assistivas que usam sintetizadores de fala específicos do idioma, portanto, é importante identificar corretamente o idioma principal do formulário para garantir que os formulários sejam lidos no idioma desejado.

Se o texto (ou texto alternativo) dos formulários for apresentado em mais de um idioma, você deverá identificar as áreas do formulário em que é feita a alternância de um idioma para outro.

No LiveCycle Designer, a configuração do idioma principal é realizada definindo a propriedade Locale do formulário e a propriedade Locale do subformulário de nível superior. Para identificar alterações no idioma principal, altere a propriedade Locale para qualquer objeto que use um idioma diferente do idioma do formulário.

Para definir a propriedade Locale de um formulário:
1. Escolha Arquivo > Propriedades do formulário e selecione a guia Padrão
2. Selecione o idioma apropriado para a Localidade do Formulário (veja a Figura 17)
3. Clique em OK

![Alterando a Localidade do Formulário na caixa de diálogo Propriedades do Formulário](/help/forms/using/assets/image-17.png)

Figura 17: **Alterando a localidade do formulário na caixa de diálogo Propriedades do formulário**

Para definir a propriedade Local do subformulário de nível superior ou de um objeto que exija um idioma diferente:
1. Selecionar o subformulário de nível superior ou o objeto no modo design
1. Exiba a paleta Objeto escolhendo Janela > Objeto
1. Na paleta Object, selecione a guia Field e, na lista Locale, selecione o idioma a ser usado para o objeto (consulte a Figura 18). Ao aplicar opções de localidade diferentes a objetos individuais, lembre-se de que os objetos que estão dentro de tabelas e subformulários recebem automaticamente a mesma configuração de localidade que o objeto de tabela e subformulário.

![Alterando a localidade de um objeto](/help/forms/using/assets/image-18.png)

Figura 18: **Alterando a localidade de um objeto**

**Pontos de verificação relacionados**:
* WCAG 1.0
   * 4.1 Identifique claramente as alterações na linguagem natural do texto de um documento e quaisquer equivalentes em texto (por exemplo, legendas).
* WCAG 2.0
   * 3.1.1 Idioma da página: o idioma humano padrão de cada página da Web pode ser determinado programaticamente. (Nível A)
   * 3.1.2 Idioma de partes: A linguagem humana de cada passagem ou frase no conteúdo pode ser determinada programaticamente, exceto por nomes próprios, termos técnicos, palavras de linguagem indeterminada e palavras ou frases que se tornaram parte do vernáculo do texto imediatamente adjacente. (Nível AA)
