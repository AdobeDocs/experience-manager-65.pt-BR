---
title: Diretrizes e as práticas recomendadas de acessibilidade para criar formulários no designer de formulários
description: Práticas recomendadas e diretrizes para acessibilidade ao desenvolver formulários no designer de formulários.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 38fb132f0eb5b710745db11e7ddf59efc0f0ae95
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 1%

---

# Mapeamento entre diretrizes e práticas recomendadas

As seções a seguir mapeiam a Seção 508 e as diretrizes da WCAG para as práticas recomendadas descritas neste guia.

## § 1194.21 Descrição das diretrizes e práticas recomendadas

### Seção 508 §1194.21: Aplicativos de software e sistemas operacionais

| § 1194.21 Orientação | Descrição da diretriz | Práticas recomendadas do LiveCycle Designer para conformidade | Notas |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| a) | Quando osoftwareé concebido para funcionar num sistema que tem um teclado, as funções do produto devem ser executáveis a partir de um teclado em que a própria função ou o resultado da execução de uma função possam ser discernidos textualmente. | <li> 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado </li><li> 2.6 Verifique se a leitura e a ordem das guias estão corretas</li> | |
| b) | As aplicações não devem perturbar nem desativar as funcionalidades ativadas de outros produtos identificados como características de acessibilidade, caso essas características sejam desenvolvidas e documentadas de acordo com os padrões do setor. Os aplicativos também não devem interromper nem desativar os recursos ativados de qualquer sistema operacional identificados como recursos de acessibilidade nos casos em que a interface de programação de aplicativos para esses recursos de acessibilidade tenha sido documentada pelo fabricante do sistema operacional e esteja disponível para o desenvolvedor do produto. | Nenhuma técnica específica do LiveCycle Designer - esta diretriz é tratada pela Adobe Reader para o PDF forms. | |
| c) | Deve ser fornecida uma indicação bem definida no ecrã do foco atual que se desloca entre os elementos da interface interativa à medida que o foco de entrada muda. O foco deve ser exposto de forma programática para que a tecnologia assistiva possa rastrear as alterações de foco e foco. | 2.3 Escolha os controles certos Para garantir que o foco seja exposto de forma programática e visual, sempre use os controles padrão. | |
| d) | As tecnologias de assistência devem dispor de informações suficientes sobre um elemento da interface do utilizador, incluindo a identidade, o funcionamento e o estado do elemento. Quando uma imagem representa um elemento de programa, as informações transmitidas pela imagem também devem estar disponíveis no texto. | <ul><li>2.1 Mantenha os formulários simples e fáceis de usar</li> <li>2.1.1 Evite mover, piscar ou piscar o conteúdo</li> <li>2.2 Configurar as propriedades do formulário para gerar informações de acessibilidade</li> <li>2.5 Fornecer rótulos adequados para controles de formulário</li></ul> | |
| e) | Quando são utilizadas imagens bitmap para identificar controlos, indicadores de estado ou outros elementos programáticos, o significado atribuído a essas imagens deve ser coerente ao longo do desempenho de uma aplicação. | <ul><li>2.4 Fornecer equivalentes de texto para imagens</li><li> 2.5 Forneça etiquetas apropriadas para os controles de formulário. Este padrão só se aplica se você usar a mesma imagem em vários locais em um formulário. O uso de controles personalizados baseados em imagem não é recomendado. Em vez disso, use somente os controles padrão fornecidos pelo LiveCycle Designer. Se você usar imagens em seus controles, sempre verifique se elas são usadas de forma consistente.</li> | |
| f) | A informação textual deve ser fornecida através das funções do sistema operacional para visualização do texto. A informação mínima que deve ser disponibilizada é o conteúdo do texto, o local do cursor de entrada de texto e os atributos do texto. | 2.3 Escolha os controles corretos Evite usar imagens para transmitir informações textuais. Em vez de usar componentes de entrada personalizados que podem não expor as propriedades de texto corretamente ao sistema operacional, sempre use os controles padrão. | |
| g) | As aplicações não devem sobrepor-se às seleções de contraste e de cores selecionadas pelo utilizador nem a outros atributos de visualização individuais. | Nenhuma técnica específica do LiveCycle Designer | Sempre que possível, use as cores básicas e padrão do sistema. |
| h) | Quando a animação é exibida, a informação deve ser apresentada em, pelo menos, um modo de apresentação não animado, por opção do utilizador. | 2.1 Mantenha os formulários simples e fáceis de usar Evite usar animações nos formulários ou forneça versões separadas nas quais as animações sejam substituídas por imagens estáticas. | |
| i) | A codificação por cores não deve ser utilizada como único meio de transmissão de informações, indicação de uma ação, solicitação de resposta ou distinção de um elemento visual. | 2.8 Usar a cor com responsabilidade | |
| j) | Quando um produto permite que um utilizador ajuste as regulações de cor e contraste, deve prever-se uma variedade de seleções de cores capazes de produzir uma gama de níveis de contraste. | Não aplicável | Essa funcionalidade geralmente é fornecida pelo Adobe Reader, não pelo desenvolvedor de formulários. |
| k) | O software não deve utilizar textos, objetos ou outros elementos intermitentes ou intermitentes com frequência de intermitência superior a 2 Hz e inferior a 55 Hz. | 2.1.1 Evite mover, piscar ou piscar o conteúdo | |
| l) | Quando são utilizados formulários eletrônicos, o formulário deve permitir que as pessoas que utilizam a tecnologia assistiva acessem as informações, os elementos de campo e a funcionalidade necessária para o preenchimento e envio do formulário, incluindo todas as direções e dicas. | 2.5 Fornecer rótulos adequados para controles de formulário | |

### Seção 508 §11942: Intranet baseada na Web e informações e aplicações da Internet

| §11942 Orientação | Descrição da diretriz | Práticas recomendadas do LiveCycle Designer para conformidade | Notas |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| a) | Um equivalente em texto para cada elemento não textual deve ser fornecido (por exemplo, por meio de &quot;alt&quot;, &quot;longdesc&quot; ou no conteúdo do elemento). | 2.4 Fornecer equivalentes de texto para imagens | |
| b) | As alternativas equivalentes para qualquer apresentação multimédia devem ser sincronizadas com a apresentação. | 2.12 Garantir que todo o conteúdo multimídia esteja acessível | |
| c) | As páginas Web devem ser concebidas de modo a que todas as informações transmitidas a cores também estejam disponíveis sem cor, por exemplo, a partir de um contexto ou de uma marcação. | 2.8 Usar a cor com responsabilidade | |
| d) | Os documentos devem ser organizados de modo a poderem ser lidos sem necessidade de uma folha de estilos associada. | Não aplicável | |
| e) | Devem ser fornecidos links de texto redundantes para cada região ativa de um mapa de imagem do lado do servidor. | Não aplicável | |
| f) | Devem ser fornecidos mapas de imagens do lado do cliente em vez de mapas de imagens do lado do servidor, exceto se as regiões não puderem ser definidas com uma forma geométrica disponível. | Não aplicável | |
| g) | Os cabeçalhos de linha e coluna devem ser identificados para os quadros de dados. | 2.9 Fornecer células de cabeçalho para tabelas | |
| h) | A marcação deve ser utilizada para associar células de dados e células de cabeçalho a tabelas de dados que tenham dois ou mais níveis lógicos de cabeçalhos de linhas ou colunas. | 2.9 Fornecer células de cabeçalho para tabelas | |
| i) | Os quadros devem ser intitulados com texto que facilite a identificação e a navegação dos quadros. | Não aplicável | |
| j) | As páginas devem ser concebidas de modo a evitar a cintilação do ecrã com uma frequência superior a 2 Hz e inferior a 55 Hz. | 2.1 Mantenha os formulários simples e fáceis de usar | |
| k) | Deve ser disponibilizada uma página apenas de texto, com informações ou funcionalidades equivalentes, para que um sítio Web cumpra as disposições da presente parte, caso a conformidade não possa ser assegurada de outra forma. O conteúdo da página &quot;apenas texto&quot; deve ser atualizado sempre que a página principal for alterada. | Não aplicável | |
| l) | Quando as páginas utilizam linguagens de script para exibir conteúdo ou criar elementos de interface, as informações fornecidas pelo script devem ser identificadas com um texto funcional que possa ser lido pela tecnologia assistiva. | 2.11 Evitar scripts com interrupções | |
| m) | Quando uma página da Web exige que um applet, plug-in ou outro aplicativo esteja presente no sistema cliente para interpretar o conteúdo da página, a página deve fornecer um link para um plug-in ou applet que esteja em conformidade com o §1194.21(a) a (l). | Não aplicável | Páginas da Web vinculadas a PDF forms devem fornecer um link para o Adobe Reader. |
| n) | Quando os formulários eletrônicos são projetados para serem preenchidos on-line, o formulário deve permitir que as pessoas que usam a tecnologia assistiva acessem as informações, os elementos de campo e a funcionalidade necessária para o preenchimento e envio do formulário, incluindo todas as direções e dicas. | 2.5 Fornecer rótulos adequados para controles de formulário | |
| o) | Deve ser fornecido um método que permita aos utilizadores pular ligações de navegação repetitivas. | 2.10 Fornecer uma estrutura de formulário navegável | |
| p) | Quando for necessária uma resposta cronometrada, o utilizador deve ser alertado e dispor de tempo suficiente para indicar que é necessário mais tempo. | 2.11 Evitar scripts com interrupções | |

### Pontos de verificação de prioridade 1 da WCAG 1.0

| Ponto de verificação | Descrição do ponto de verificação | Práticas recomendadas do LiveCycle Designer para conformidade | Notas |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | Forneça um equivalente em texto para cada elemento não textual (por exemplo, por meio de &quot;alt&quot;, &quot;longdesc&quot; ou no conteúdo do elemento). Isso inclui: imagens, representações gráficas de texto (incluindo símbolos), regiões de mapa de imagem, animações (por exemplo, GIF animados), applets e objetos programáticos, arte ASCII, quadros, scripts, imagens usadas como marcadores de lista, espaçadores, botões gráficos, sons (reproduzidos com ou sem interação do usuário), arquivos de áudio independentes, faixas de áudio de vídeo e vídeo. | <ul><li>2.4 Fornecer equivalentes de texto para imagens</li> <li>2.12 Garantir que todo o conteúdo multimídia esteja acessível</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | Forneça links de texto redundantes para cada região ativa de um mapa de imagem do lado do servidor. | Não aplicável | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | Até que os agentes do usuário possam ler automaticamente em voz alta o equivalente em texto de uma faixa visual, forneça uma descrição auditiva das informações importantes da faixa visual de uma apresentação multimídia. | 2.12 Garantir que todo o conteúdo multimídia esteja acessível | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | Para qualquer apresentação multimídia baseada em tempo (por exemplo, um filme ou uma animação), sincronize alternativas equivalentes (por exemplo, legendas ou descrições auditivas da faixa visual) com a apresentação. | 2.12 Garantir que todo o conteúdo multimídia esteja acessível | |
| [2.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | Verifique se todas as informações transmitidas com a cor também estão disponíveis sem cor, por exemplo, do contexto ou da marcação. | 2.8 Usar a cor com responsabilidade | |
| [4.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | Identifique claramente as alterações no idioma natural do texto de um documento e quaisquer equivalentes de texto (por exemplo, legendas). | 2.13 Identificar alterações na linguagem | |
| [5.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | Para tabelas de dados, identifique cabeçalhos de linhas e colunas. | 2.9 Fornecer células de cabeçalho para tabelas | |
| [5.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | Para tabelas de dados que tenham dois ou mais níveis lógicos de cabeçalhos de linha ou coluna, use a marcação para associar células de dados e células de cabeçalho. | 2.9 Fornecer células de cabeçalho para tabelas | |
| [6.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | Organize documentos para que eles possam ser lidos sem folhas de estilos. Por exemplo, quando um documento HTML é renderizado sem as folhas de estilos associadas, ainda deve ser possível ler o documento. | Não aplicável | |
| [6.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | Verifique se os equivalentes para conteúdo dinâmico são atualizados quando o conteúdo dinâmico é alterado. | 2.11 Evitar scripts com interrupções | |
| [6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | Certifique-se de que as páginas sejam utilizáveis quando scripts, applets ou outros objetos programáticos estiverem desativados ou não forem suportados. Se isso não for possível, forneça informações equivalentes em uma página alternativa acessível. | 2.11 Evitar scripts com interrupções | |
| [7.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | Até que os agentes do usuário permitam que os usuários controlem a oscilação, evite fazer com que a tela pisque. | 2.1 Mantenha os formulários simples e fáceis de usar | |
| [9.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | Fornecer mapas de imagem do lado do cliente em vez de mapas de imagem do lado do servidor, exceto quando as regiões não puderem ser definidas com uma forma geométrica disponível. | Não aplicável | |
| [11.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | Se, depois de todos os esforços, você não conseguir criar uma página acessível, forneça um link para uma página alternativa que use tecnologias W3C, seja acessível, tenha informações equivalentes (ou funcionalidade) e seja atualizada sempre que a página inacessível (original). | Não aplicável | |
| [12.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | Coloque um título em cada quadro para facilitar a identificação e a navegação. | Não aplicável | |
| [14.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | Use a linguagem mais clara e simples apropriada para o conteúdo de um site. | 2.1 Mantenha os formulários simples e fáceis de usar | |

### Pontos de verificação de prioridade 2 da WCAG 1.0

| Ponto de verificação de prioridade 2 | Descrição do ponto de verificação | Práticas recomendadas do LiveCycle para conformidade | Notas |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | Verifique se as combinações de cores do primeiro plano e do plano de fundo fornecem contraste suficiente quando visualizadas por alguém com déficits de cores ou quando visualizadas em uma tela preta e branca. [Prioridade 2 para imagens, Prioridade 3 para texto]. | 2.8 Usar a cor com responsabilidade | |
| [3.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | Quando existir um idioma de marcação apropriado, use a marcação em vez de imagens para transmitir as informações. | <ul><li>2.1 Mantenha os formulários simples e fáceis de usar</li><li> 2.1.1 Evite mover, piscar ou piscar o conteúdo</li> <li>2.2 Configure as propriedades do formulário para gerar informações de acessibilidade Sempre use o texto real em vez de imagens de texto.</li> | |
| [3.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | Crie documentos que validam gramáticas formais publicadas. | | Os PDF forms devem corresponder à especificação de PDF publicada para serem renderizados no Adobe Reader. |
| [3.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | Use folhas de estilos para controlar o layout e a apresentação. | Não aplicável | |
| [3.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | Use unidades relativas em vez de absolutas nos valores de atributo da linguagem de marcação e valores de propriedade da folha de estilos. | Não aplicável | |
| [3.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | Use elementos de cabeçalho para transmitir a estrutura do documento e usá-los de acordo com as especificações. | 2.10 Fornecer uma estrutura de formulário navegável | |
| [3.6](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | Marque listas e itens de lista corretamente. | 2.10.3 Listas de marcação Marque o conteúdo baseado em lista como listas usando as funções Lista e Item de lista. | |
| [3.7](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | Marcar cotações. Não use a marcação de aspas para formatar efeitos como recuo. | Não aplicável | |
| [5.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | Não use tabelas para layout, a menos que a tabela faça sentido quando linearizada. Caso contrário, se a tabela não fizer sentido, forneça um equivalente alternativo (que pode ser uma versão linearizada). | Nenhuma técnica de LiveCycle específica | Não há motivo para usar tabelas para layout em formulários de LiveCycle. Em vez disso, use a paleta Layout para posicionar os campos de formulário em um padrão de grade. Use uma tabela somente quando utilizar recursos específicos da tabela, como cabeçalhos da tabela. |
| [5.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | Se uma tabela for usada para layout, não use nenhuma marcação estrutural para fins de formatação visual. | Nenhuma técnica de LiveCycle específica | |
| [6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | Para scripts e applets, certifique-se de que os manipuladores de eventos sejam independentes de dispositivos de entrada. | 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado | |
| [6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | Certifique-se de que o conteúdo dinâmico esteja acessível ou forneça uma apresentação ou página alternativa. | 2.11 Evitar scripts com interrupções | |
| [7.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | Até que os agentes do usuário permitam que os usuários controlem a intermitência, evite fazer com que o conteúdo pisque (ou seja, alterar a apresentação em uma taxa regular, como ativar e desativar). | 2.1 Mantenha os formulários simples e fáceis de usar | |
| [7.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | Até que os agentes do usuário permitam que os usuários congelem a movimentação de conteúdo, evite a movimentação nas páginas. | 2.1 Mantenha os formulários simples e fáceis de usar | |
| [7.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | Até que os agentes do usuário forneçam a capacidade de interromper a atualização, não crie periodicamente páginas de atualização automática. | Não aplicável | |
| [7.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | Até que os agentes do usuário forneçam a capacidade de interromper o redirecionamento automático, não use a marcação para redirecionar páginas automaticamente. Em vez disso, configure o servidor para executar redirecionamentos. | Não aplicável | |
| [8.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | Torne elementos programáticos, como scripts e applets diretamente acessíveis ou compatíveis com tecnologias assistivas [Prioridade 1 se a funcionalidade for importante e não for apresentada em outro lugar; caso contrário, Prioridade 2.] | 2.11 Evitar scripts com interrupções | |
| [9.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | Certifique-se de que qualquer elemento que tenha sua própria interface possa ser operado de maneira independente de dispositivo. | 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado | |
| [9.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | Para scripts, especifique manipuladores de eventos lógicos em vez de manipuladores de eventos dependentes de dispositivo. | 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado | |
| [10.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | Até que os agentes do usuário permitam que os usuários desativem as janelas geradas, não faça com que janelas pop-ups ou outras janelas sejam exibidas e não altere a janela atual sem informar o usuário. | 2.11 Evitar scripts com interrupções | |
| [10.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | Até que os agentes do usuário suportem associações explícitas entre rótulos e controles de formulário, para todos os controles de formulário com rótulos implicitamente associados, verifique se o rótulo está posicionado corretamente. | 2.5 Fornecer rótulos adequados para controles de formulário | |
| [11.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | Use as tecnologias W3C quando elas estiverem disponíveis e forem apropriadas para uma tarefa e use as versões mais recentes quando houver suporte. | Não aplicável | |
| [11.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | Evite recursos obsoletos das tecnologias W3C. | Não aplicável | |
| [12.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | Descreva a finalidade dos quadros e como eles se relacionam entre si, se não for óbvio somente pelos títulos dos quadros. | Não aplicável | |
| [12.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | Dividir grandes blocos de informações em grupos mais gerenciáveis onde for natural e apropriado. | 2.10 Fornecer uma estrutura de formulário navegável | |
| [12.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | Associar rótulos explicitamente a seus controles. | 2.5 Fornecer rótulos adequados para controles de formulário | |
| [13.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | Identifique claramente o target de cada link. | 2.5 Fornecer rótulos adequados para controles de formulário 2.5.6 Fornecer texto do link | |
| [13.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | Forneça metadados para adicionar informações semânticas a páginas e sites. | Não aplicável | |
| [13,3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | Forneça informações sobre o layout geral de um site (por exemplo, um mapa de site ou índice). | 2.10 Fornecer uma estrutura de formulário navegável | |
| [13,4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | Use os mecanismos de navegação de maneira consistente. | 2.10 Fornecer uma estrutura de formulário navegável | Use páginas mestras para criar conteúdo de navegação consistente. |

### Critérios de sucesso da WCAG 2.0

| Pontos de verificação prioritários 1 G 2 | Práticas recomendadas do LiveCycle para conformidade | Notas |
| --- | --- | --- |
| 1.1 [Alternativas de texto](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [Conteúdo não textual](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 Fornecer equivalentes de texto para imagens | |
| | 2.5 Fornecer rótulos adequados para controles de formulário | |
| 1.2 [Mídia com base no tempo](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [Apenas áudio e apenas vídeo (pré-gravado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.2 [Legendas (pré-gravadas)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.3 [Descrição de áudio ou alternativa de mídia (pré-gravada)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.4 [Legendas (ao vivo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.5 [Descrição de áudio (pré-gravado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.6 [Linguagem de sinais (pré-gravada)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.7 [Descrição de áudio estendido (pré-gravado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.8 [Alternativa de mídia (pré-gravada)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.2.9 [Somente áudio (ao vivo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 Garantir que todo o conteúdo de áudio e vídeo esteja acessível | |
| 1.3 [Adaptável](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [Informações e Relações](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 Fornecer células de cabeçalho para tabelas | |
| 1.3.2 [Sequência significativa](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 Verifique se a leitura e a ordem das guias estão corretas | |
| | 2.10 Fornecer uma estrutura de formulário navegável | |
| 1.3.3 [Características sensoriais](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 Usar a cor com responsabilidade | |
| 1.4 [Discernível](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [Uso de cor](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 Usar a cor com responsabilidade | |
| 1.4.2 [Controle de áudio](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | Nenhuma técnica de LiveCycle específica | |
| 1.4.3 [Contraste (Mínimo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 Usar a cor com responsabilidade | |
| 1.4.4 [Redimensionar texto](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | Nenhuma técnica de LiveCycle específica | |
| 1.4.5 [Imagens de texto](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | Nenhuma técnica de LiveCycle específica | |
| 1.4.6 [Contraste (Avançado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 Usar a cor com responsabilidade | |
| 1.4.7 [Áudio de fundo baixo ou sem](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | Nenhuma técnica de LiveCycle específica | |
| 1.4.9 [Imagens de texto (sem exceção)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | Nenhuma técnica de LiveCycle específica | |
| 2.1 [Acessível por teclado](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [Teclado](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 Verifique se a leitura e a ordem das guias estão corretas | |
| | 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado | |
| 2.1.2 [Nenhuma armadilha de teclado](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado | |
| 2.1.3 [Teclado (Sem Exceção)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 Verifique se a leitura e a ordem das guias estão corretas | |
| | 2.7 Garantir que os controles de formulário estejam acessíveis ao teclado | |
| 2.2 [Tempo suficiente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [Tempo ajustável](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | Nenhuma técnica de LiveCycle específica | |
| 2.2.2 [Pausar, Interromper, Ocultar](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 Mantenha os formulários simples e fáceis de usar | |
| 2.2.3 [Sem Tempo](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | Nenhuma técnica de LiveCycle específica | |
| 2.2.4 [Interrupções](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | Nenhuma técnica de LiveCycle específica | |
| 2.2.5 [Reautenticação](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | Nenhuma técnica de LiveCycle específica | |
| 2.3 [Convulsões] | | |
| 2.3.1 [Três Flashes ou Abaixo do Limite](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 Mantenha os formulários simples e fáceis de usar | |
| 2.3.2 [Três Flashes](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 Mantenha os formulários simples e fáceis de usar | |
| 2.4 [Navegável](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [Ignorar blocos](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 Fornecer uma estrutura de formulário navegável | |
| 2.4.2 [Página com título](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | Nenhuma técnica de LiveCycle específica | |
| 2.4.3 [Ordem de foco](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 Verifique se a leitura e a ordem das guias estão corretas | |
| 2.4.4 [Finalidade do link (em contexto)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | Nenhuma técnica de LiveCycle específica | A finalidade do link depende de os autores escolherem texto significativo para elementos vinculados. |
| 2.4.5 [Várias maneiras](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 Fornecer uma estrutura de formulário navegável | |
| 2.4.6 [Títulos e rótulos](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 Fornecer rótulos adequados para controles de formulário</li><li>2.10 Fornecer uma estrutura de formulário navegável</li> | |
| 2.4.7 [Foco visível](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | Nenhuma técnica de LiveCycle específica | O foco padrão em formulários de LiveCycle é visível. |
| 2.4.8 [Localização](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | Nenhuma técnica de LiveCycle específica | Não aplicável: os formulários LiveCycle não exigem sistemas de navegação. |
| 2.4.9 [Finalidade do link (somente link)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | Nenhuma técnica de LiveCycle específica | A finalidade do link depende de os autores escolherem texto significativo para elementos vinculados. |
| 2.4.10 [Cabeçalhos da seção](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 Fornecer uma estrutura de formulário navegável | |
| 3.1 [Legível](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [Idioma da página](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 Identificar a linguagem natural e quaisquer alterações na linguagem | |
| 3.1.2 [Idioma de Partes](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 Identificar a linguagem natural e quaisquer alterações na linguagem | |
| 3.1.3 [Palavras incomuns](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | Nenhuma técnica de LiveCycle específica | |
| 3.1.4 [Abreviações](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | Nenhuma técnica de LiveCycle específica | |
| 3.1.5 [Nível de leitura](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | Nenhuma técnica de LiveCycle específica | |
| 3.1.6 [Pronúncia](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | Nenhuma técnica de LiveCycle específica | |
| 3.2 [Previsível](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [Em foco](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 Evitar scripts com interrupções | |
| 3.2.2 [Na entrada](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 Evitar scripts com interrupções | |
| 3.2.3 [Navegação consistente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 Fornecer uma estrutura de formulário navegável | |
| 3.2.4 [Identificação consistente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 Escolha os controles certos</li><li>2.5 Fornecer rótulos adequados para controles de formulário</li> | |
| 3.2.5 [Alteração mediante solicitação](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 Evitar scripts com interrupções | |
| 3.3 [Assistência de entrada](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [Identificação de erro](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | O LiveCycle Designer fornece ferramentas para marcar campos de formulário conforme necessário e executar a validação de entrada de formulário. |
| 3.3.2 [Etiquetas ou Instruções](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 Fornecer rótulos adequados para controles de formulário | |
| 3.3.3 [Sugestão de erro](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | O LiveCycle Designer fornece ferramentas para marcar campos de formulário conforme necessário e executar a validação de entrada de formulário. |
| 3.3.4 [Prevenção de erros (legal, financeiro, dados)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | Nenhuma técnica de LiveCycle específica | |
| 3.3.5 [Ajuda](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | Nenhuma técnica de LiveCycle específica | |
| 3.3.6 [Prevenção de erros (todos)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | Nenhuma técnica de LiveCycle específica | |
| 4.1 [Compatível](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [Análise](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | Nenhuma técnica de LiveCycle específica | |
| 4.1.2 [Nome, Função, Valor](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 Escolha os controles certos</li> <li>2.5 Fornecer rótulos adequados para controles de formulário</li> | |



