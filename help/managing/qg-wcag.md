---
title: Guia rápido para WCAG 2.0
seo-title: Guia rápido para WCAG 2.0
description: Leia uma rápida visão geral das diretrizes de acessibilidade do WCAG 2.0.
seo-description: Leia uma rápida visão geral das diretrizes de acessibilidade do WCAG 2.0.
uuid: a5cf463e-89e9-4cc0-9c91-69a1fd3d8ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-accessibility
content-type: reference
discoiquuid: 3cac0e34-7514-48ce-a93b-592bbdbcd252
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Guia rápido para WCAG 2.0{#quick-guide-to-wcag}

O AEM foi desenvolvido para maximizar a conformidade com as Diretrizes de acessibilidade do conteúdo da Web:

As [Web Content Accessibility Guidelines versão 2.0 (WCAG2)](https://www.w3.org/TR/WCAG/) são um conjunto de diretrizes reconhecidas internacionalmente desenvolvidas pelo [World Wide Web Consortium (W3C)](https://www.w3.org/) sob sua [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

O WCAG 2.0 consiste em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável para pessoas com necessidades especiais. Prestam aconselhamento aos autores, designers e desenvolvedores de conteúdos Web, a fim de garantir que os recursos que produzem sejam o mais acessíveis possível ao maior número possível de pessoas, independentemente de qualquer deficiência que tenham; por exemplo, deficiência visual, perda auditiva, dificuldades de aprendizagem, limitações relacionadas com a idade, entre outras.

Por exemplo, descrever uma imagem (ou qualquer outro conteúdo não textual) usando o `alt` atributo em HTML beneficia muito as pessoas que são cegas ou amblíopes. A descrição textual no `alt` atributo pode ser convertida em saída de fala ou transmitida para exibições em braille eletrônicas atualizáveis.

Além disso, o WCAG 2.0 pode resultar em vantagens para outros beneficiários, incluindo pessoas que podem ser consideradas *com deficiência* situacional. Pessoas que, devido a circunstâncias como a tecnologia de navegação, a velocidade de conexão da rede ou o ambiente de navegação, podem enfrentar barreiras semelhantes às pessoas com deficiências.

Usando o Adobe Experience Manager, os autores de conteúdo e/ou proprietários de sites podem criar conteúdo da Web que atenda aos critérios relevantes de sucesso do Nível A e do Nível AA do WCAG 2.0.

Portanto, entender os objetivos do WCAG 2.0 e como as diretrizes são estruturadas é uma parte importante do entendimento da acessibilidade da Web e como as diretrizes podem ajudar na criação de conteúdo da Web acessível.

A intenção da WCAG 2.0 é fornecer diretrizes que:

* São **agnósticos tecnológicos:**

   Em outras palavras, orientações que podem ser aplicadas a diversos formatos de conteúdo da Web, não apenas HTML. Assim, o WCAG 2.0 pode abranger o conteúdo gerado ou fornecido em PDF, Flash, JavaScript e outras tecnologias da Web atuais e futuras. O objetivo é resolver uma deficiência reconhecida do WCAG 1.0, na medida em que o foco era no HTML, em detrimento de outros formatos de conteúdo da Web.

* São **testáveis:**

   Cada orientação é redigida de forma a poder ser objetivamente testada, a fim de garantir que um grupo de peritos em matéria de acessibilidade concordasse, de um modo geral, que a orientação foi cumprida. Um dos desafios das orientações em matéria de acessibilidade é que, embora algumas possam ser testadas tecnicamente, outras exigem uma avaliação humana para determinar se a orientação foi ou não cumprida com êxito. O WCAG 2.0 foi escrito com o objetivo de reduzir a subjetividade que estava presente em algumas das diretrizes e pontos de verificação do WCAG 1.0.

* Suporte **priorizado e implementação contextual:**

   Tal como acontece com o WCAG 1.0, as orientações do WCAG 2.0 são prioritárias, relacionadas com o impacto provável de não seguir uma orientação para um grupo específico de utilizadores com deficiência. Isto permite aos autores tomar uma decisão informada sobre as orientações mais importantes para a sua situação específica. Além disso, é introduzido o conceito de *acessibilidade suportado* . Isso permite que os autores tomem decisões sobre como usar as tecnologias da Web que podem não ter suporte total à acessibilidade, ou exigir que os usuários tenham tecnologias de assistência e/ou navegadores específicos para se beneficiarem dos recursos de acessibilidade.

Estes objetivos influenciaram significativamente a estrutura da WCAG 2.0.

>[!NOTE]
>
>Não é possível criar um site que atenda a qualquer deficiência ou tipo de pessoa possível. O objetivo do WCAG 2.0 é ajudar os autores da Web a criar sites que sejam, na medida do possível, acessíveis em determinadas condições e dentro dos limites da razão.

>[!NOTE]
>
>Se estiver familiarizado com o WCAG 1.0, você observará algumas alterações no WCAG 2.0. Estes dizem respeito ao âmbito, à organização e ao objetivo.

## Estrutura {#structure}

O WCAG 2.0 está estruturado de uma forma que introduz conceitos de criação de conteúdo web acessível de forma progressivamente detalhada. Isso pode dar a impressão de que o WCAG 2.0 é um conjunto muito complexo de documentos interligados, mas o objetivo é (progressivamente) fornecer informações mais detalhadas conforme e quando os autores precisarem - em vez de fornecer tudo isso em um documento muito grande.

O WCAG 2.0 consiste em quatro princípios chave para um design acessível. São eles:

1. **Percebível**: um usuário pode sentir o conteúdo da Web em questão?
1. **Operável**: um usuário pode navegar, inserir dados ou interagir com o conteúdo da Web?
1. **Compreendido**: um usuário pode processar e compreender o conteúdo da Web apresentado a ele?
1. **Robusto**: o conteúdo da Web está disponível da maneira desejada em uma ampla variedade de ambientes de navegação, incluindo ambientes de navegação antigos e emergentes?

Estes princípios são por vezes referidos pela sigla POUR.

* Cada **princípio** consiste numa ou mais **orientações**.

   * As diretrizes são escritas como instruções, que são positivas (Faça isso...) ou negativas (Não faça isso...).
   * As orientações são numeradas de 1.1 a 4.1, quando o primeiro número corresponde ao princípio da empresa-mãe.

* Cada orientação consiste em um ou mais critérios **de** sucesso.

   * Os critérios de sucesso são escritos como declarações, que são `True` ou `False` para qualquer página da Web.
   * Os critérios de sucesso podem incluir opções ou opções, ou podem incluir exceções; situações em que os critérios de sucesso não têm de ser cumpridos.
   * Os critérios de sucesso são numerados de acordo com a orientação e o princípio da empresa-mãe, de 1.1.1 a 4.1.1. Eles também têm um nome curto resumindo a intenção do critério, para uma referência mais fácil. Por exemplo, o critério de sucesso 1.1.1 é alternativo não textual.
   * Os critérios de sucesso incluem uma lista de **técnicas** relacionadas (descritas em mais detalhes abaixo).

## Recursos de suporte {#supporting-resources}

Além dos componentes principais do WCAG 2.0 de Princípios, Orientações e Critérios de Sucesso, há uma série de documentos comprovativos. Alguns deles fornecem conselhos específicos sobre como cumprir aspectos das diretrizes, outros são referências mais gerais que ajudam autores da Web, designers e desenvolvedores de todas as habilidades a entender e usar o WCAG 2.0 da forma mais eficiente possível.

Embora o WCAG 2.0 seja um documento estável e não seja alterado, a maioria desses recursos de suporte são documentos dinâmicos; eles mudarão e crescerão com o tempo, à medida que novas tecnologias surgirem, e novos exemplos de como a acessibilidade da Web pode ser alcançada.

### Recursos do WCAG 2.0 {#wcag-resources}

* [Um resumo de todos os documentos](https://www.w3.org/WAI/intro/wcag.php)relacionados com o WCAG 2.0;
* [Explicação da relação entre os diferentes componentes](https://www.w3.org/WAI/intro/wcag20);
* [Perguntas](https://www.w3.org/WAI/WCAG20/wcag2faq.html)frequentes sobre o WCAG 2.0;

### Técnicas para WCAG 2.0 {#techniques-for-wcag}

As técnicas para WCAG 2.0 estão disponíveis na página [Técnicas para WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/) .

**As técnicas** formam o nível abaixo dos critérios de sucesso na hierarquia do WCAG 2.0. Eles são classificados pela WAI como informativos, não normativos. Por outras palavras, não é necessário seguir uma técnica específica para que um recurso esteja em conformidade com o WCAG 2.0.

Como as técnicas são muito mais específicas do que os critérios de sucesso, elas geralmente se referem a uma tecnologia ou tipo de conteúdo específico (por exemplo, HTML ou vídeo), ou situação (por exemplo, comércio eletrônico ou aplicativo de e-learning). Você pode considerar técnicas como exemplos comprovados de como diretrizes específicas e critérios de sucesso podem ser cumpridos, de modo que elas são úteis para autores e desenvolvedores que trabalham em contextos específicos.

As técnicas podem ser acessadas:

* Por coleção (as técnicas podem ser gerais ou estar relacionadas a uma tecnologia ou formato específico - como HTML, CSS ou Scripts do cliente), ou
* De critérios de sucesso relacionados. As técnicas podem se aplicar a mais de um critério de sucesso.

Cada técnica tem um número exclusivo, que se relaciona à sua coleção. Por exemplo, uma das técnicas ARIA é a *Técnica ARIA2: Identificação de campos obrigatórios com a propriedade*&quot;obrigatório&quot;.

As técnicas podem ser suficientes, consultivas ou uma falha:

* Uma técnica *suficiente* é uma que, se for seguida, será suficiente para satisfazer um critério de sucesso específico.
* Uma técnica ** consultiva é uma que, se for seguida, terá um impacto positivo na acessibilidade, mas pode não ser suficiente por si só para garantir que um critério específico de sucesso seja cumprido.
* Uma *falha* é uma técnica que descreve um exemplo específico de onde um critério de sucesso não seria atendido.

Os detalhes das técnicas incluem uma descrição, aplicabilidade, exemplos, recursos para obter mais informações e detalhes sobre como os autores podem testar a aplicação bem-sucedida da técnica.

A lista de técnicas não está completa e a WAI está constantemente atualizando a lista com novos exemplos, refletindo desenvolvimentos na tecnologia da Web, abordagens de design e resultados de pesquisa. Portanto, vale a pena verificar regularmente a lista de técnicas para novos aditamentos.

### Noções básicas sobre o WCAG 2.0 {#understanding-wcag}

Trata-se de uma série de documentos, que fornecem conselhos que ajudam os leitores a apreciar o objetivo de orientações específicas e critérios de sucesso. Você pode [baixar uma introdução, além de links para informações](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/Overview.html)mais detalhadas.

Cada orientação individual e critério de sucesso tem também a sua própria página &quot;Compreensão&quot;, que fornece informações sobre:

* A intenção da orientação;
* Critérios de sucesso específicos;
* Técnicas de aconselhamento, que ajudam a cumprir os requisitos da orientação, mas que não se enquadram em nenhum critério específico de sucesso.

Cada página de &quot;entendimento&quot; individual de cada critério de sucesso fornece informações sobre:

* A intenção do critério de sucesso;
* Exemplos gerais de como o critério de sucesso pode ser cumprido;
* Recursos relacionados (não W3C) sobre como cumprir o critério de sucesso;
* Técnicas e falhas: exemplos específicos e detalhados de como o critério de sucesso pode ser atendido (descritos em mais detalhes abaixo)
* Termos principais - um glossário de termos importantes para entender o critério de sucesso.

Um exemplo pode ser encontrado em: [Noções sobre o Critério de sucesso 1.1.1 (&quot;Conteúdo não textual&quot;)](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/text-equiv-all.html).

### Como cumprir o WCAG 2.0 {#how-to-meet-wcag}

A seção &quot;Como cumprir&quot; está disponível na página [Como cumprir o WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/) . Esta seção fornece uma apresentação alternativa da WCAG, que permite refinar o conteúdo das orientações para os mais relevantes para os interesses ou circunstâncias do próprio leitor. Os leitores podem filtrar as técnicas de critérios de sucesso que desejam visualizar especificando tecnologias de conteúdo da Web específicas, como planilhas de estilo em cascata ou scripts, ou especificando um ou mais níveis de prioridade.

Sem filtragem, esse recurso fornece todos os critérios de sucesso agrupados por orientação. Para cada critério de sucesso, é fornecido o seguinte:

* O texto do critério de sucesso;
* Uma ligação ao documento de &quot;entendimento&quot; correspondente;
* Lista das técnicas suficientes conexas, ligando-se aos pormenores de cada técnica;
* Uma lista das técnicas consultivas conexas, ligando-as aos pormenores de cada técnica (se existir);
* Uma lista de falhas relacionadas, vinculando aos detalhes de cada falha.