---
title: Criação de conteúdo acessível para o Adobe Experience Manager (Conformidade com o WCAG 2.1)
description: Usar o AEM para ajudar a tornar o conteúdo da Web acessível e utilizável por pessoas com deficiência
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '13630'
ht-degree: 81%

---

# Criação de conteúdo acessível (Conformidade com o WCAG 2.1) {#creating-accessible-content-wcag-conformance}

As [Diretrizes de Acessibilidade de Conteúdo da Web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), elaboradas por [um grupo de trabalho do World Wide Web Consortium](https://www.w3.org/groups/#Accessibility_Guidelines_Working_Group), consistem em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável por pessoas com deficiência.

Como introdução, o consórcio fornece uma série de seções e documentos de apoio:

* [Novos recursos na WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Como cumprir a WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Noções básicas sobre a WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Técnicas da WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Os documentos da WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Além disso, consulte:
* O [Guia Rápido para a WCAG 2.1](/help/managing/qg-wcag.md).
* Os [Relatórios de conformidade para acessibilidade de soluções da Adobe](https://www.adobe.com/accessibility/compliance.html).
* [Configurar o Editor de Rich Text para a produção de conteúdo acessível](/help/sites-administering/rte-accessible-content.md)

As diretrizes são classificadas de acordo com os três níveis de conformidade: Nível A (o mais baixo), Nível AA e Nível AAA (o mais alto). Em resumo, os níveis são definidos da seguinte maneira:

* **Nível A**: o site atinge um nível mínimo básico de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A são cumpridos.
* **Nível AA:** esse é um nível ideal de acessibilidade que você deve almejar, no qual seu site atinge um nível fundamental de acessibilidade, de forma a ser acessível para a maioria das pessoas na maior parte das situações usando a maioria das tecnologias. Para atingir esse nível, todos os Critérios de sucesso do Nível A e Nível AA são cumpridos.
* **Nível AAA:** O site atinge um nível muito elevado de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A, Nível AA e Nível AAA devem ser cumpridos.

Ao criar o seu site, é necessário determinar o nível global com o qual você gostaria que ele estivesse em conformidade.

A seção a seguir apresenta as [camadas das Diretrizes da WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) com os critérios de sucesso relacionados aos [níveis de conformidade](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A e AA.

>[!NOTE]
>
>Neste documento, é usado o seguinte:
>
>* [Os nomes curtos das Diretrizes da WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* [A numeração usada nas Diretrizes da WCAG 2.1](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) para auxiliar na referência cruzada com o site da WCAG.

## Princípio 1: perceptível       {#principle-perceivable}

[Princípio 1: perceptível - As informações e os componentes da interface do usuário têm de ser apresentados aos usuários de formas perceptíveis.](https://www.w3.org/TR/WCAG/#perceivable)

### Alternativas em texto (1.1)       {#text-alternatives}

[Diretriz 1.1 Alternativas em texto: Fornece alternativas em texto para qualquer conteúdo não textual, para que seja possível alterá-lo para outras formas mais adequadas à necessidade do indivíduo, como impressão em caracteres ampliados, braille, fala, símbolos ou linguagem mais simples.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Conteúdo não textual (1.1.1) {#non-text-content}

* Critério de Sucesso 1.1.1
* Nível A
* Conteúdo não textual: todo o conteúdo não textual que é apresentado ao usuário tem uma alternativa em texto que serve um propósito equivalente, exceto para as situações indicadas abaixo.

#### Finalidade - Conteúdo não textual (1.1.1) {#purpose-non-text-content}

As informações de uma página da web podem ser fornecidas em vários formatos não textuais diferentes, como imagens, vídeos, animações, tabelas e gráficos. Pessoas cegas ou que possuem deficiências visuais graves não conseguem visualizar um conteúdo não textual. No entanto, o conteúdo do texto pode ser acessado por meio de um leitor de tela ou apresentado em formato tátil por um dispositivo de exibição em Braille. Portanto, ao fornecer alternativas em texto ao conteúdo no formato gráfico, as pessoas que não puderem ver o conteúdo gráfico podem acessar uma versão equivalente das informações que o conteúdo fornece.

Uma vantagem adicional é que as alternativas em texto permitem que o conteúdo não textual seja indexado pela tecnologia do mecanismo de pesquisa.

#### Como cumprir - Conteúdo não textual (1.1.1) {#how-to-meet-non-text-content}

Para gráficos estáticos, o requisito básico é o de proporcionar uma alternativa em texto equivalente para o gráfico. Isso pode ser feito no campo **Texto alternativo**. Consulte, por exemplo, o Componente principal **[Imagem](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=pt-BR)**.

>[!NOTE]
>
>Alguns Componentes principais predefinidos, como **[Carrossel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=pt-BR)**, não fornecem um campo **Texto alternativo** para adicionar descrições de texto alternativo a imagens individuais, embora exista o campo **Rótulo** (guia **[Acessibilidade](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=pt-BR#accessibility-tab)**) para o componente inteiro.
>
>Ao implementar as versões desses componentes na instância do AEM, a equipe de desenvolvimento precisará configurá-los para serem compatíveis com o atributo `alt`, de forma que os autores possam adicioná-lo ao conteúdo (consulte [Adição de suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

Por padrão, o AEM requer que o campo **Texto alternativo** seja preenchido. Se a imagem for meramente decorativa e um texto alternativo não for necessário, será possível marcar a opção **A imagem é decorativa**.

#### Criar boas alternativas de texto {#creating-good-text-alternatives}

Existem várias formas de conteúdo não textual, portanto, o valor da alternativa em texto depende da função que o gráfico desempenha na página da Web. Algumas regras básicas gerais a serem seguidas:

* As alternativas em texto devem ser sucintas, mas devem capturar claramente as informações essenciais fornecidas pelo conteúdo não textual.
* Descrições excessivamente longas (mais de 100 caracteres) devem ser evitadas. Se um texto alternativo exigir mais detalhes:
   * forneça uma breve descrição no texto alternativo
   * e inclua uma descrição de texto mais longa em outro lugar na mesma página ou em uma página da web separada. Insira um link para essa descrição separada na imagem ou no texto adjacente à imagem.
* O texto alternativo não deve replicar o conteúdo fornecido no formulário de texto próximo à mesma página. Lembre-se de que muitas imagens são ilustrações de pontos já abordados no texto de uma página, portanto, pode existir uma alternativa em texto detalhado.
* Se o conteúdo não textual for um link para outra página ou documento e não houver outro texto fazendo parte do mesmo link, o texto alternativo para a imagem deverá indicar o destino do link. Ele não deve descrever a imagem.
* Se o conteúdo não textual estiver contido em um elemento de botão e não houver texto fazendo parte do mesmo botão, o texto alternativo da imagem deverá indicar a funcionalidade do botão. Ele não deve descrever a imagem.
* É perfeitamente aceitável deixar o texto alternativo de uma imagem em branco (nulo), mas somente se ela não precisar de um texto alternativo. Por exemplo, se for um gráfico meramente decorativo ou se um texto equivalente estiver presente no texto da página.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Tipos específicos de conteúdo não textual que necessitam de alternativas em texto podem incluir:

* Fotos ilustrativas: são imagens de pessoas, objetos ou lugares. É importante pensar na função da foto na página e descrever o conteúdo da imagem, já que a tecnologia de assistência anunciará o tipo de elemento (por exemplo, `graphic` ou `image`). Pode aumentar a clareza usar `screenshot` ou `illustration` nas descrições de texto alternativo, mas isso depende do contexto. A consistência é um fator importante. Uma decisão deve ser tomada pela equipe de criação, e isso deve ser aplicado à inteira experiência do usuário.
* Ícones: são pequenos pictogramas (gráficos) que transmitem informações específicas. Eles devem ser usados de forma consistente em uma página e um site. Todas as instâncias do ícone em uma página ou um site devem ter a mesma alternativa em texto curta e sucinta, a menos que isso resulte em duplicação desnecessária do texto adjacente.
* Tabelas e gráficos: geralmente representam dados numéricos. Portanto, uma opção para fornecer uma alternativa em texto pode ser incluir um breve resumo das principais tendências mostradas no gráfico. Se necessário, também forneça uma descrição mais detalhada no texto usando o campo **Descrição** na guia de propriedades de imagem **Avançado**. Além disso, é possível fornecer os dados de origem em forma de tabela em outro lugar da página ou site.
* Mapas, diagramas, fluxogramas: para gráficos que fornecem dados espaciais (por exemplo, para permitir a descrição das relações entre objetos ou um processo), verifique se a mensagem principal é fornecida em formato de texto e se essa informação sobre o texto está posicionada perto de cada ponto de dados associado. Para mapas, fornecer um equivalente de texto completo provavelmente não será prático, mas se o mapa for fornecido como uma maneira de ajudar as pessoas a encontrar o caminho para um determinado local, o texto alternativo da imagem do mapa poderá indicar brevemente a informação *Mapa de X* e, em seguida, fornecer instruções para acessar esse local no texto de outro lugar da página ou por meio do campo **Descrição** na guia **Avançado** do componente **Imagem**.
* CAPTCHAs: Um CAPTCHA é um *teste de Turing público completamente automatizado para diferenciação entre computadores e humanos*. É uma verificação de segurança usada em páginas da Web para distinguir os humanos de softwares mal-intencionados, mas que pode causar barreiras de acessibilidade. São imagens que exigem que os usuários descrevam o que eles veem para passar em um teste de segurança. Fornecer uma alternativa em texto para a imagem não é possível. Em vez disso, considere usar soluções não gráficas alternativas. O W3C fornece algumas sugestões, como:
   * Enigmas de lógica
   * O uso de som em vez de imagens
   * Contas e filtros de spam de uso limitado.
* Imagens de fundo: são obtidas usando Cascading Style Sheets (CSS) em vez de HTML. Isso significa que não é possível especificar um valor de texto alternativo. Portanto, as imagens de fundo não devem fornecer informações textuais importantes; se o fizerem, essas informações também deverão ser disponibilizadas no texto da página. No entanto, é importante que um fundo alternativo seja mostrado quando a imagem não puder ser exibida.

>[!NOTE]
>
>Deve haver um nível adequado de contraste entre o plano de fundo e o texto de primeiro plano; isso é abordado com mais detalhes na seção [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Mais informações - Conteúdo não contextual (1.1.1) {#more-information-non-text-content}

* [Noções sobre o Critério de sucesso 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Como cumprir o Critério de sucesso 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Explicação do W3C sobre as alternativas para CAPTCHAs](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Mídia com base no tempo (1.2)       {#time-based-media}

[Diretriz de mídia com base no tempo 1.2: fornece alternativas para a mídia com base no tempo.](https://www.w3.org/TR/WCAG/#time-based-media)

Trata-se de um conteúdo da Web que é *baseado no tempo*. Isso abrange o conteúdo que o usuário pode reproduzir (como vídeo, áudio e conteúdo animado) e pode ser pré-gravado ou ter transmissão ao vivo.

### Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Critério de sucesso 1.2.1
* Nível A
* Apenas áudio e apenas vídeo (pré-gravado): para mídia somente de áudio e somente de vídeo pré-gravada, as informações a seguir são verdadeiras, exceto quando o áudio ou vídeo for uma alternativa em mídia para o texto e for claramente identificado como tal:
   * Apenas áudio pré-gravado: é fornecida uma alternativa para mídia baseada no tempo que apresenta informações equivalentes para conteúdo apenas áudio pré-gravado.
   * Somente vídeo pré-gravado: é fornecida uma alternativa para mídia baseada em tempo ou uma faixa de áudio que apresenta informações equivalentes para conteúdo apenas de vídeo pré-gravado.

#### Propósito - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Algumas pessoas podem enfrentar problemas de acessibilidade em vídeos e áudios, como:

* Pessoas com deficiências visuais em casos onde não há trilha sonora ou esta não é suficiente para informá-las do que está acontecendo no vídeo ou animação;
* Pessoas com deficiências auditivas ou surdas, que não conseguem ouvir a trilha sonora;
* Pessoas que podem ouvir a trilha sonora, mas não entendem o que está sendo falado (por exemplo, porque está em um idioma que não entendem).

O vídeo ou áudio também pode estar indisponível para pessoas que usam navegadores ou dispositivos que não são compatíveis com a reprodução de conteúdo em formatos de mídia específicos, como o Adobe Flash.

Fornecer essas informações em um formato diferente, como texto (ou áudio para vídeos sem áudio), pode torná-las acessíveis para pessoas que não conseguem acessar o conteúdo original.

#### Como cumprir - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Se o conteúdo for um áudio pré-gravado sem vídeo (como um podcast):
   * Forneça um link imediatamente antes ou depois do conteúdo para obter uma transcrição do texto do conteúdo de áudio. A transcrição deve ser uma página HTML com uma versão em texto equivalente de todo o conteúdo falado, bem como de um conteúdo não falado que seja importante, além de incluir uma indicação de quem está falando, uma descrição do cenário, expressões vocais e uma descrição de qualquer outro áudio relevante.
* Se o conteúdo for uma animação ou vídeo pré-gravado sem áudio:
   * Forneça um link imediatamente antes ou depois do conteúdo para uma descrição de texto equivalente das informações fornecidas no vídeo
   * Ou uma descrição de áudio equivalente em um formato de áudio usado com frequência, como MP3.

>[!NOTE]
>
>Se o conteúdo de áudio ou vídeo for fornecido como uma alternativa para um conteúdo que já existe em outro formato na mesma página da web, uma alternativa adicional pode não ser necessária.
>
>As orientações em [Entenda a WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html) fornecem mais informações.

Inserir multimídia em suas páginas da Web do AEM é semelhante à inserção de uma imagem. No entanto, como o conteúdo multimídia é muito mais do que uma imagem estática, há várias configurações e opções diferentes para controlar a forma como a multimídia é reproduzida.

>[!NOTE]
>
>Ao usar multimídia com um conteúdo informativo, é necessário criar também links para as alternativas. Por exemplo, para incluir uma transcrição de texto, crie uma página HTML para exibir a transcrição e, em seguida, adicione um link ao lado ou abaixo do conteúdo de áudio.

#### Mais informações - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Noções sobre o Critério de sucesso 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Como cumprir o Critério de sucesso 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Legendas (pré-gravadas) (1.2.2) {#captions-prerecorded}

* Critério de sucesso 1.2.2
* Nível A
* Legendas (pré-gravadas): as legendas são disponibilizadas para todo o conteúdo de áudio pré-gravado na multimídia sincronizada, exceto quando a mídia é uma alternativa para texto e é claramente identificada como tal.

#### Propósito - Legendas (pré-gravadas) (1.2.2) {#purpose-captions-prerecorded}

Os indivíduos surdos ou com deficiência auditiva não conseguirão ou terão grande dificuldade ao acessar o conteúdo de áudio. As legendas são equivalentes em texto para áudio falado e não falado, exibidas na tela no momento adequado durante o vídeo. Elas permitem que os indivíduos que não conseguem ouvir o áudio entendam o que está acontecendo.

#### Como cumprir - Legendas (pré-gravadas) (1.2.2) {#how-to-meet-captions-prerecorded}

As legendas podem ser:

* Abertas: sempre visíveis quando o vídeo é reproduzido
* Ocultas: as legendas podem ser ativadas ou desativadas pelo usuário

Use legendas ocultas sempre que possível, pois elas oferecem ao usuário a opção de visualizar legendas. 

Para as legendas ocultas, crie e forneça um arquivo de legenda sincronizada em um formato apropriado (como [SMIL](https://www.w3.org/AudioVideo/)), junto com o arquivo de vídeo (os detalhes sobre como proceder estão fora do escopo desse guia, mas fornecemos links para alguns tutoriais em [Mais informações - Legendas (pré-gravadas) (1.2.2)](#more-information-captions-prerecorded)). Certifique-se de fornecer uma nota ou habilitar o recurso de legenda no player de vídeo para informar aos usuários que legendas estão disponíveis para o vídeo.

Se você precisar usar legendas abertas, incorpore o texto à faixa de vídeo. Isso pode ser feito usando aplicativos de edição de vídeo que permitem a sobreposição de títulos no vídeo.

#### Mais informações - Legendas (pré-gravadas) (1.2.2) {#more-information-captions-prerecorded}

* [Noções sobre o Critério de sucesso 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [Como cumprir o Critério de sucesso 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Critério de Sucesso 1.2.3
* Nível A
* Descrição de áudio ou alternativa de mídia (pré-gravada): uma alternativa para mídias com base no tempo ou uma descrição de áudio do conteúdo de vídeo pré-gravado é fornecida para a mídia sincronizada, exceto quando a mídia é uma alternativa para o texto e é claramente identificada como tal.

#### Propósito - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Os indivíduos que são cegos ou deficientes visuais vão enfrentar barreiras de acessibilidade se as informações em um vídeo ou uma animação forem fornecidas apenas visualmente, ou se a trilha sonora não fornecer informações suficientes para permitir a compreensão do que está acontecendo visualmente.

#### Como cumprir - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Há duas abordagens que podem ser adotadas para atender a esse critério de sucesso. Ambas são aceitáveis:

1. Incluir uma descrição de áudio adicional para o conteúdo de vídeo. Isso pode ser feito por uma de três maneiras:
   * Durante as pausas na caixa de diálogo existente, forneça informações sobre as alterações na cena que não são apresentadas como parte da faixa de áudio existente;
   * Forneça uma faixa de áudio nova, adicional e opcional que contenha a trilha sonora original, mas incluindo também informações de áudio extras sobre as mudanças de cena.
      * Os usuários podem alternar entre a faixa de áudio existente (que *não* contém uma descrição de áudio) e a nova faixa de áudio (que *contém* uma descrição de áudio).
      * Isso evita a interrupção para usuários que não precisam de uma descrição adicional.
   * Crie uma segunda versão do conteúdo de vídeo para permitir descrições de áudio mais extensas. Isso reduz as dificuldades associadas ao fornecimento de descrições de áudio detalhadas dentro das lacunas do diálogo existente, pausando temporariamente o áudio e o vídeo em pontos apropriados. Como resultado, uma descrição de áudio muito mais longa pode ser fornecida, antes de retornar à ação. Como no exemplo anterior, a melhor forma de fornecer essa opção é disponibilizar uma faixa de áudio extra opcional, para evitar a interrupção de usuários que não precisam de uma descrição adicional.
1. Forneça uma transcrição de texto que seja um equivalente de texto adequado dos elementos visuais e de áudio do vídeo ou da animação. Isso deve incluir, quando apropriado, uma indicação de quem está falando, uma descrição do cenário, quaisquer eventos ou informações apresentados visualmente, além das expressões vocais. Dependendo do tamanho, você pode colocar a transcrição na mesma página do vídeo ou animação ou em uma página separada; caso escolha a última opção, forneça um link para a transcrição ao lado do vídeo ou animação.

Detalhes exatos de como criar um vídeo descrito por áudio estão fora do escopo desse guia. A criação de descrições de vídeo e áudio pode ser demorada, mas outros produtos da Adobe podem ajudar a realizar essas tarefas.

#### Mais informações - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Noções sobre o Critério de sucesso 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Como cumprir o Critério de sucesso 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Legendas (ao vivo) (1.2.4)              {#captions-live}

* Critério de sucesso 1.2.4
* Nível AA
* Legendas (ao vivo): são fornecidas legendas para todo o conteúdo de áudio ao vivo na mídia sincronizada.

#### Propósito - Legendas (ao vivo) (1.2.4)       {#purpose-captions-live}

Esse critério de sucesso é idêntico às [Legendas (pré-gravadas)](#captions-prerecorded), já que aborda as barreiras de acessibilidade enfrentadas pelos indivíduos surdos ou com deficiências auditivas, exceto que esse critério de sucesso lida com as apresentações ao vivo, como webcasts.

#### Como cumprir - Legendas (ao vivo) (1.2.4) {#how-to-meet-captions-live}

Siga as orientações fornecidas acima para [Legendas (pré-gravadas)](#captions-prerecorded). No entanto, por se tratar de uma mídia com conteúdo ao vivo, as legendas devem ser criadas o mais rápido possível e em resposta ao que está acontecendo. Portanto, você deve considerar o uso de legendas em tempo real ou ferramentas de fala para texto.

Instruções detalhadas estão além do escopo desse documento, mas os seguintes recursos disponibilizam informações úteis:

* [WebAIM: legendagem em tempo real](https://webaim.org/techniques/captions/realtime)

* [Projeto AccessComputing (University of Washington): as legendas podem ser geradas automaticamente usando reconhecimento de voz?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### Mais informações - Legendas (ao vivo) (1.2.4)       {#more-information-captions-live}

* [Noções sobre o Critério de sucesso 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Como cumprir o Critério de sucesso 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Descrição de áudio (pré-gravado) (1.2.5)  {#audio-description-prerecorded}

* Critério de Sucesso 1.2.5
* Nível AA
* Descrição de áudio (pré-gravado): uma descrição de áudio é fornecida para todo o conteúdo de vídeo pré-gravado na mídia sincronizada.

#### Propósito - Descrição de áudio (pré-gravado) (1.2.5) {#purpose-audio-description-prerecorded}

Esse critério de sucesso é idêntico à [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-prerecorded), exceto que os autores devem fornecer uma descrição de áudio muito mais detalhada para estar em conformidade com o Nível AA.

#### Como cumprir - Descrição de áudio (pré-gravado) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Siga as orientações fornecidas para a [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-prerecorded).

#### Mais informações - Descrição de áudio (pré-gravado) (1.2.5) {#more-information-audio-description-prerecorded}

* [Noções sobre o Critério de sucesso 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Como cumprir o Critério de sucesso 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptável (1.3)       {#adaptable}

[Diretriz 1.3 Adaptável: crie conteúdo que possa ser apresentado de maneiras diferentes (por exemplo, layout mais simples) sem perder informações ou estrutura.](https://www.w3.org/TR/WCAG/#adaptable)

Esta diretriz abrange os requisitos necessários para fornecer suporte a pessoas que:

* pode não ser capaz de acessar as informações apresentadas por um autor na apresentação padrão desse conteúdo (por exemplo, um layout de várias colunas ou uma página com uso intenso de cores e/ou imagens).

* usam uma exibição visual alternativa ou apenas de áudio, como um texto grande ou contraste alto.

### Informações e Relações (1.3.1)              {#info-and-relationships}

* Critério de Sucesso 1.3.1
* Nível A
* Informações e relacionamentos: as informações, a estrutura e os relacionamentos transmitidos por meio da apresentação podem ser determinados de forma programática ou estão disponíveis no texto.

#### Propósito - Informações e Relações (1.3.1)       {#purpose-info-and-relationships}

Muitas tecnologias assistivas utilizadas por pessoas com deficiência contam com informações estruturais para exibir ou *compreender* o conteúdo de forma eficiente. Essas informações estruturais podem assumir a forma de cabeçalhos de página, cabeçalhos de linha e coluna de tabela e tipos de lista. Por exemplo, um leitor de tela pode permitir que um usuário navegue por uma página de cabeçalho em cabeçalho. No entanto, caso a estrutura do conteúdo da página pareça depender exclusivamente do estilo visual, em vez do HTML subjacente, não haverá informações estruturais disponíveis para as tecnologias de acessibilidade e sua capacidade de facilitar a navegação será limitada.

Esse critério de sucesso existe para garantir que a informação estrutural seja fornecida programaticamente via HTML, ou outras técnicas de codificação, de modo que os navegadores e as tecnologias de assistência possam acessar e aproveitar as informações.

#### Como cumprir - Informações e Relações (1.3.1)       {#how-to-meet-info-and-relationships}

O AEM facilita a criação de um conteúdo da web semanticamente significativo usando os elementos HTML apropriados. Abra o conteúdo da página no RTE (um componente de Texto) e use o menu **Formatar parágrafo** (símbolo de parágrafo) para especificar o elemento estrutural apropriado (por exemplo, parágrafo e cabeçalho).

É possível verificar se as suas páginas da web têm a estrutura adequada usando os seguintes elementos, quando aplicável:

* **Cabeçalhos:** contanto que os recursos de acessibilidade do RTE estejam habilitados, o AEM oferece três níveis de cabeçalho de página. É possível usá-los para identificar seções e subseções de conteúdo. O cabeçalho 1 é o nível mais alto, o Cabeçalho 3 o mais baixo. O administrador do sistema pode configurar o sistema para permitir o uso de mais níveis de cabeçalho.

* **Listas**: você pode usar HTML para especificar três tipos diferentes de listas:
   * O elemento `<ul>` é usado para listas *desordenadas* (com marcadores). Os itens da lista individual são identificados usando o elemento `<li>`. No RTE, use o ícone **Lista de marcadores**.
   * O elemento `<ol>` é usado para as listas *numeradas*. Os itens da lista individual são identificados usando o elemento `<li>`. No RTE, use o ícone **Lista numerada**.

  Se desejar alterar o conteúdo existente em um tipo de lista específica, destaque o texto e selecione o tipo de lista apropriado. Como no exemplo anterior que mostra como o texto do parágrafo é inserido, os elementos de lista apropriados são adicionados automaticamente ao HTML.

  No modo de tela cheia, os ícones **Lista com marcadores** e **Lista numerada** ficam visíveis. Quando não estiver no modo de tela cheia, as duas opções estarão disponíveis no ícone **Listas**.

* **Tabelas**: Tabelas de dados devem ser identificadas usando os elementos da tabela de HTML:
   * um elemento `<table>`
   * um elemento `<tr>` para cada linha da tabela
   * um elemento `<th>` para cada linha e cabeçalho da coluna
   * um elemento `<td>` para cada célula de dados

  Além disso, as tabelas acessíveis usam os seguintes elementos e atributos:

   * O elemento `<caption>` é usado para fornecer uma legenda visível para a tabela. Por padrão, as legendas são exibidas de forma centralizada acima da tabela, mas podem ser posicionadas adequadamente usando CSS. A legenda é associada à tabela de forma programada, portanto, é um método útil para fornecer uma introdução ao conteúdo.
   * O elemento `<summary>` auxilia os usuários com deficiências visuais a compreender de forma mais fácil as informações apresentadas em uma tabela, fornecendo um resumo do que pode ser visto. Isso é útil quando layouts complexos ou não convencionais são usados (esse atributo não é exibido no navegador, somente é lido nas tecnologias de assistência).
   * O `scope` atributo do elemento `<th>` é usado para indicar se uma célula representa um cabeçalho de uma linha ou de uma coluna específica. Uma abordagem semelhante é a de usar o cabeçalho e os atributos de id em tabelas complexas, onde as células de dados podem ser associadas a um ou mais cabeçalhos.

  >[!NOTE]
  >
  >Por padrão, esses elementos e atributos não estão diretamente disponíveis, embora o administrador do sistema possa adicionar o suporte para esses valores na caixa de diálogo **Propriedades da tabela** (consulte [Adicionar suporte para outros elementos e atributos do HTML](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

  Para abrir a caixa de diálogo **Tabela** onde é possível selecionar a guia **Propriedades da tabela**:

   * Defina uma **Legenda** adequada.
   * Remova qualquer valor padrão para **Largura**, **Altura**, **Borda**, **Preenchimento da célula e** **Espaçamento entre células**. já que essas propriedades podem ser definidas em uma planilha de estilos global.

  Em seguida, você pode usar a opção **Propriedades da célula** para escolher entre uma célula de dados ou de cabeçalho:

* **Ênfase**: Use o elemento `<strong>` ou `<em>` para indicar ênfase. Não use os cabeçalhos para destacar o texto dentro dos parágrafos.
   * Destaque o texto que deseja enfatizar;
   * Clique no ícone **B** (para `<strong>`) ou no ícone **I** (para `<em>`) exibido no painel **Propriedades** (verifique se o HTML está selecionado).

     >[!NOTE]
     >
     >O RTE em uma instalação padrão do AEM está configurado para usar:
     >
     >* `<b>` para `<strong>`
     >* `<i>` para `<em>`
     >
     >Eles são efetivamente os mesmos, mas `<strong>` e `<em>` são preferíveis, pois são html semanticamente corretos. Sua equipe de desenvolvimento pode configurar o RTE para usar `<strong>` e `<em>` (em vez de `<b>` e `<i>`), ao desenvolver a instância do projeto.

* **Tabelas de Dados Complexos**: às vezes, quando há tabelas complexas com dois ou mais níveis de cabeçalhos, as Propriedades da Tabela básicas podem não ser suficientes para fornecer todas as informações estruturais necessárias. Para esses tipos de tabelas complexas, relações diretas devem ser criadas entre os cabeçalhos e suas células relacionadas usando os atributos **cabeçalho** e **id**.

  >[!NOTE]
  >
  >O atributo de ID não está disponível em uma instalação predefinida. Ele pode ser habilitado configurando regras de HTML e o serializador no RTE.

  Por exemplo, na tabela abaixo os cabeçalhos e IDs são combinados para fazer uma associação programática para usuários de tecnologia assistiva.

  ```xml
    <table>
      <tr>
        <th rowspan="2" id="h">Homework</th>
        <th colspan="3" id="e">Exams</th>
        <th colspan="3" id="p">Projects</th>
      </tr>
      <tr>
        <th id="e1" headers="e">1</th>
        <th id="e2" headers="e">2</th>
        <th id="ef" headers="e">Final</th>
        <th id="p1" headers="p">1</th>
        <th id="p2" headers="p">2</th>
        <th id="pf" headers="p">Final</th>
      </tr>
      <tr>
        <td headers="h">15%</td>
        <td headers="e e1">15%</td>
        <td headers="e e2">15%</td>
        <td headers="e ef">20%</td>
        <td headers="p p1">10%</td>
        <td headers="p p2">10%</td>
        <td headers="p pf">15%</td>
      </tr>
    </table>
  ```

  Para obter isso no AEM, adicione a marcação diretamente usando o modo de edição de origem.

  >[!NOTE]
  >
  >Essa funcionalidade não está imediatamente disponível em uma instalação padrão. Ela requer a configuração do RTE, das regras de HTML e do serializador.

#### Mais informações - Informações e Relações (1.3.1) {#more-information-info-and-relationships}

* [Noções sobre o Critério de sucesso 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Como cumprir o Critério de sucesso 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Sequência significativa (1.3.2)  {#meaningful-sequence}

* Critério de Sucesso 1.3.2
* Nível A
* Sequência significativa: quando a sequência na qual o conteúdo é apresentado afeta seu significado, uma sequência de leitura correta pode ser determinada programaticamente.

#### Propósito - Sequência significativa (1.3.2) {#purpose-meaningful-sequence}

O propósito deste critério de sucesso é permitir que um agente do usuário forneça uma apresentação alternativa do conteúdo, preservando a ordem de leitura necessária para entender o significado. É importante que seja possível determinar programaticamente pelo menos uma sequência do conteúdo que faça sentido. Um conteúdo que não atende a esse critério de sucesso pode confundir ou desorientar os usuários quando a tecnologia de acessibilidade ler o conteúdo na ordem errada ou quando forem aplicadas planilhas de estilo alternativas ou outras alterações de formatação.

#### Como cumprir - Sequência significativa (1.3.2) {#how-to-meet-meaningful-sequence}

Siga as orientações em [Como cumprir o Critério de sucesso 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Mais informações - Sequência significativa (1.3.2) {#more-information-meaningful-sequence}

* [Noções sobre o Critério de sucesso 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Como cumprir o Critério de sucesso 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Características sensoriais (1.3.3)              {#sensory-characteristics}

* Critério de Sucesso 1.3.3
* Nível A
* Características sensoriais: as instruções fornecidas para compreender e utilizar o conteúdo não dependem somente das características sensoriais dos componentes, como forma, tamanho, localização visual, orientação ou som.

#### Propósito - Características sensoriais (1.3.3)       {#purpose-sensory-characteristics}

Ao apresentar as informações, os designers geralmente se concentram nos recursos de design visual, como cor, forma, estilo de texto ou a posição relativa/absoluta de uma parte do conteúdo. Estas podem ser técnicas de design muito eficientes na transmissão de informações (e podem melhorar a acessibilidade geral para usuários com visão, mas que possuem necessidades de acessibilidade cognitiva), porém, pessoas cegas ou deficientes visuais podem não conseguir acessar informações que exigem a identificação visual de atributos como posição, cor ou forma.

Da mesma forma, as informações que exigem a distinção entre sons diferentes (por exemplo, o conteúdo falado com voz masculina ou feminina) apresentam barreiras de acessibilidade para os indivíduos com deficiência auditiva, se não estiverem refletidas em nenhuma alternativa em texto para o conteúdo de áudio.

>[!NOTE]
>
>Para os requisitos relacionados às alternativas de cor, consulte [Uso de cor](#use-of-color).

#### Como cumprir - Características sensoriais (1.3.3)       {#how-to-meet-sensory-characteristics}

Certifique-se de que todas as informações que dependem das características visuais do conteúdo da página também sejam apresentadas em um formato alternativo.

* Não se baseie na posição visual para fornecer informações. Por exemplo, se você quiser que os usuários acessem um menu no lado direito da página para obter mais informações, não consulte *o menu à direita*; em vez disso, nomeie o menu (por exemplo, por meio de um cabeçalho) e faça referência a esse nome no texto.
* Não se baseie no estilo do texto (por exemplo, negrito ou itálico) como a única maneira de transmitir as informações.

>[!NOTE]
>
>O uso de termos descritivos são aceitáveis se forem entendidos como tendo significado em um contexto não visual. Por exemplo, usar as palavras *acima* e *abaixo* geralmente é aceitável, uma vez que implicam, respectivamente, em um conteúdo antes e depois de um determinado item do conteúdo. Isso ainda faria sentido se o conteúdo fosse falado em voz alta.

#### Mais informações - Características sensoriais (1.3.3)       {#more-information-sensory-characteristics}

* [Noções sobre o Critério de sucesso 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Como cumprir o Critério de sucesso 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Discernível (1.4)       {#distinguishable}

[Diretriz 1.4 Discernível: facilitar a visualização e a audição de conteúdos aos usuários, incluindo a separação do primeiro plano e do plano de fundo. ](https://www.w3.org/TR/WCAG/#distinguishable)

### Utilização de cor (1.4.1)              {#use-of-color}

* Critério de Sucesso 1.4.1
* Nível A
* Utilização de cor: a cor não é usada como o único meio visual de transmitir informações, indicar uma ação, solicitar uma resposta ou distinguir um elemento visual.

>[!NOTE]
>
>Esse critério de sucesso aborda especificamente a percepção da cor. Outras formas de percepção são abordadas na [Adaptável (1.3)](#adaptable), incluindo o acesso programático a cores e outras codificações de apresentação visual.

#### Propósito - Utilização de cor (1.4.1)       {#purpose-use-of-color}

As cores são uma forma eficaz de melhorar o apelo estético das páginas da web e também são úteis na transmissão de informações. No entanto, existem diversas deficiências visuais, desde a cegueira até o daltonismo, que podem impedir algumas pessoas de distinguir certas cores. Devido a isso, a codificação por cores não é um método eficaz de se disponibilizar informações. 

Por exemplo, alguém com deficiência de visão de cor vermelho-verde não será capaz de distinguir entre tons de verde e tons de vermelho. É possível que ele veja as duas cores como uma terceira cor (por exemplo, marrom). Nesse caso, o indivíduo não conseguirá distinguir entre vermelho, verde e marrom.

Além disso, a cor pode não ser observada por indivíduos que usam navegadores somente de texto, dispositivos com visor monocromático ou que utilizam uma impressão em preto e branco da página.

Uma outra consideração é o estado *seleted* para um elemento de interface (por exemplo, guias, botões de alternância, entre outros), que deve ser transmitido de alguma forma que não seja apenas com cor e além de apenas uma apresentação visual. Para esses elementos, o uso adicional de padrões, formas e informações programáticas é útil ao criar uma experiência do usuário totalmente inclusiva que não depende de um sentido específico.

#### Como cumprir - Utilização de cor (1.4.1)       {#how-to-meet-use-of-color}

Sempre que a cor for usada para transmitir informações, certifique-se de que a informação está disponível, sem a necessidade da visualização das cores.

Por exemplo, verifique se as informações fornecidas através das cores também estão evidentes no texto.

Se a cor for usada como uma indicação para fornecer as informações, você deverá disponibilizar uma indicação visual adicional, como uma mudança de estilo (por exemplo, negrito, itálico) ou de fonte. Isso ajuda os indivíduos com problemas de visão ou daltonismo a identificar as informações. No entanto, não é possível depender dessas opções completamente, uma vez que isso não ajudará os indivíduos que não conseguem visualizar nada na página. Portanto, é (às vezes) útil fornecer texto oculto ou usar soluções programáticas, como o [pacote de padrões da Web ARIA (Accessible Rich Internet Applications)](https://www.w3.org/WAI/standards-guidelines/aria/), para transmitir essas informações a usuários sem visão.

#### Mais informações - Utilização de cor (1.4.1) {#more-information-use-of-color}

* [Noções sobre o Critério de sucesso 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Como cumprir o Critério de sucesso 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Controle de áudio (1.4.2)  {#audio-control}

* Critério de Sucesso 1.4.2
* Nível A
* Controle de áudio: se qualquer áudio em uma página da Web for reproduzido automaticamente por mais de 3 segundos, um mecanismo estará disponível para pausar ou parar o áudio, ou um mecanismo estará disponível para controlar o volume de áudio independentemente do nível geral de volume do sistema.

#### Propósito - Controle de áudio (1.4.2) {#purpose-audio-control}

As pessoas que usam software de leitura de tela podem achar difícil ouvir a saída da fala se houver outra reprodução de áudio ao mesmo tempo. Essa dificuldade é exacerbada quando a saída de voz do leitor de tela é baseada em software (como a maioria é hoje) e é regulada pelo mesmo controle de volume do som. Além disso, algumas pessoas com deficiências cognitivas e neurodivergentes podem ter sensibilidade ao som. Para essas pessoas, a incapacidade de alterar o volume do conteúdo de áudio é um fator bastante incômodo.

Portanto, é importante que o usuário possa desligar o som de fundo.

>[!NOTE]
>
>Ter controle do volume inclui a capacidade de reduzir seu volume para zero.

#### Como cumprir - Controle de áudio (1.4.2) {#how-to-meet-audio-control}

Siga as orientações em [Como cumprir o Critério de sucesso 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Mais informações - Controle de áudio (1.4.2) {#more-information-audio-control}

* [Noções sobre o Critério de sucesso 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Como cumprir o Critério de sucesso 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contraste (Mínimo) (1.4.3)       {#contrast-minimum}

* Critério de Sucesso 1.4.3
* Nível AA
* Contraste (Mínimo): a apresentação visual de texto e imagens de texto tem uma taxa de contraste de pelo menos 4,5:1, exceto para o seguinte:
   * Texto Grande: o texto em grande escala e as imagens de texto em grande escala têm uma taxa de contraste de pelo menos 3:1.
   * Incidental: o texto ou as imagens de texto que fazem parte de um componente de interface de usuário inativo, [decoração pura](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), não está visível para ninguém ou que fazem parte de uma imagem que contém outro conteúdo visual significativo, não têm requisito de contraste.
   * Logotipos: o texto que faz parte de um logotipo ou marca comercial não tem requisito de contraste.

  >[!NOTE]
  >
  >Consulte [Compreensão do contraste não textual](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) para obter mais informações e ajudar a garantir que os autores de conteúdo entendam os requisitos adicionais sobre elementos não textuais (incluindo ícones, elementos de interface, entre outros).

#### Propósito - Contraste (Mínimo) (1.4.3)       {#purpose-contrast-minimum}

Indivíduos com certas deficiências visuais podem não conseguir distinguir entre determinados pares de cores de baixo contraste. Essas pessoas podem enfrentar problemas de acessibilidade se:

* O texto contrasta mal com a cor de fundo.
* A codificação de cores do texto (como textos que contém um link e textos sem link) é importante na distinção das informações.

>[!NOTE]
>
>Textos usados exclusivamente para fins decorativos estão excluídos desse critério de sucesso.

#### Como cumprir - Contraste (Mínimo) (1.4.3)       {#how-to-meet-contrast-minimum}

Verifique se o texto está suficientemente contrastado com o plano de fundo. As relações de contraste dependem do tamanho e do estilo do texto em questão:

* Para texto com menos de 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste entre o texto/imagens de texto e o plano de fundo deve ser de pelo menos 4,5:1.
* Para texto com pelo menos 18 pontos (ou 14 pontos em negrito) em tamanho, a taxa de contraste deve ser de pelo menos 3:1.
* Se um plano de fundo for padronizado, o plano de fundo ao redor de qualquer texto deverá ser sombreado para que a proporção 4.5:1 ou 3:1 seja mantida.

>[!NOTE]
>
>Lembre-se de que as fontes podem divergir na forma como renderizam o tamanho equivalente de PT/PX/EM.
>
>Use bom senso e confira no lado da legibilidade e da usabilidade ao selecionar as fontes e o dimensionamento apropriados para o conteúdo da Web.

>[!NOTE]
>
>Os seguintes sites podem ajudar com conversões para outras unidades:
>
>* Calculadora De [Px Para Em - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* Consulte &quot;Conversão do tamanho da fonte: pixel-point-em-rem-percent&quot; em `https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/`
>* Consulte PMtoEM.com: Conversão de PX para EM simplificada em `http://pxtoem.com/`

Para verificar as relações de contraste, use uma ferramenta de contraste de cores, como o [Color Contrast Analyzer do Paciello Group](https://www.paciellogroup.com/resources/contrast-analyser.html) ou o [Color Contrast Checker do WebAIM](https://webaim.org/resources/contrastchecker/). Essas ferramentas permitem verificar pares de cores e relatar problemas de contraste.

De maneira alternativa, se não estiver tão preocupado em especificar a aparência de sua página, poderá optar por não especificar as cores do texto de primeiro e segundo plano. Nenhuma verificação de contraste é necessária, já que o navegador do usuário determina as cores do texto e plano de fundo.

Se não for possível atender aos níveis de contraste recomendados, forneça um link para uma versão alternativa e equivalente da página (que não tem problemas de contraste de cores). Ou permita que o usuário ajuste o contraste do esquema de cores da página de acordo com suas próprias necessidades.

#### Mais informações - Contraste (Mínimo) (1.4.3)       {#more-information-contrast-minimum}

* [Noções sobre o Critério de sucesso 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Como cumprir o Critério de sucesso 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Redimensionar texto (1.4.4)  {#resize-text}

* Critério de Sucesso 1.4.4
* Nível A
* Redimensionar texto: exceto em legendas e imagens de texto, o texto pode ser redimensionado sem tecnologia assistiva até 200% sem perda de conteúdo ou funcionalidade.

#### Propósito - Redimensionar texto (1.4.4) {#purpose-resize-text}

O propósito deste Critério de sucesso é garantir que o texto renderizado visualmente, incluindo controles baseados em texto (caracteres de texto que foram exibidos para que possam ser vistos [vs. caracteres de texto que ainda estejam na forma de dados como ASCII]) possam ser dimensionados com sucesso para que sejam lidos diretamente por pessoas com deficiências visuais leves, sem a necessidade do uso de tecnologia de assistência, como um ampliador de tela. Os usuários podem se beneficiar do dimensionamento de todo o conteúdo na página da Web, mas o texto é mais importante.

#### Como cumprir - Redimensionar texto (1.4.4) {#how-to-meet-resize-text}

Além de seguir as diretrizes em [Como cumprir o Critério de sucesso 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text), você pode incentivar os autores de conteúdo a usar larguras fluidas e flexíveis, além de alturas em seus designs de página e tamanhos de fonte (por exemplo, web design responsivo) para permitir que os leitores possam redimensionar o texto.

#### Mais informações - Redimensionar texto (1.4.4) {#more-information-resize-text}

* [Noções sobre o Critério de sucesso 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Como cumprir o Critério de sucesso 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Imagens de texto (1.4.5)       {#images-of-text}

* Critério de Sucesso 1.4.5
* Nível AA
* Imagens de texto: se as tecnologias usadas puderem obter a apresentação visual, o texto será usado para transmitir as informações, em vez das imagens de texto, exceto para o seguinte:
   * Personalizável: a imagem do texto pode ser personalizada visualmente de acordo com os requisitos do usuário;
   * Essencial: uma apresentação distintiva do texto é essencial para a transmissão das informações.

>[!NOTE]
>
>Os logotipos (texto que faz parte de um logotipo ou nome de marca) são considerados essenciais.

#### Propósito - Imagens de texto (1.4.5)       {#purpose-images-of-text}

Imagens de texto são usadas com frequência quando um determinado estilo de texto é preferido; por exemplo, um logotipo ou se o texto foi gerado de outra fonte (por exemplo, uma digitalização de um documento em papel). No entanto, em comparação com o texto apresentado no HTML e estilizado usando CSS, as imagens de texto não têm flexibilidade com relação à alteração de tamanho ou aparência, o que pode ser necessário para indivíduos com deficiências visuais ou dificuldade de leitura.

#### Como cumprir - Imagens de texto (1.4.5)       {#how-to-meet-images-of-text}

Se as imagens de texto tiverem que ser utilizadas, use o CSS para substituir as imagens de texto pelo texto equivalente em HTML, para que o texto seja disponibilizado de forma personalizada. Para obter um exemplo, consulte [C30: usando CSS para substituir texto por imagens de texto e fornecendo controles de interface do usuário para alternar](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Mais informações - Imagens de texto (1.4.5)       {#more-information-images-of-text}

* [Noções sobre o Critério de sucesso 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Como cumprir o Critério de sucesso 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Princípio 2: operável       {#principle-operable}

[Princípio 2: operável - os componentes da interface de usuário e a navegação precisam ser operáveis.](https://www.w3.org/TR/WCAG/#operable)

### Acessível por teclado (2.1) {#keyboard-accessible}

[Diretriz 2.1 acessível por teclado: disponibilize toda a funcionalidade de um teclado.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Isso garante que os usuários possam acessar toda a funcionalidade usando um teclado.

### Teclado (2.1.1)  {#keyboard}

* Critério de Sucesso 2.1.1
* Nível A
* Teclado: toda a funcionalidade do conteúdo é operável por meio de uma interface de teclado sem exigir tempos específicos para pressionamentos de teclas individuais, exceto quando a função subjacente requer uma entrada que depende do caminho do movimento do usuário, não apenas dos pontos finais.

#### Propósito - Teclado (2.1.1) {#purpose-keyboard}

O objetivo desse Critério de sucesso é garantir que, sempre que possível, o conteúdo possa ser operado por meio de um teclado ou a interface de teclado (para que um teclado alternativo possa ser usado). Quando o conteúdo pode ser operado por meio de um teclado ou teclado alternativo, ele é operável por pessoas sem visão (que não podem usar dispositivos como mouses, pois exigem coordenação entre olho e mão), bem como por pessoas que precisam usar teclados alternativos ou dispositivos de entrada que atuam como emuladores de teclado. Os emuladores de teclado incluem software de entrada de fala, software “sip-and-puff”, teclados virtuais, software de digitalização e uma variedade de tecnologias assistivas e teclados alternativos. As pessoas com baixa visão também podem ter dificuldade em rastrear um ponteiro e consideram o uso do software muito mais fácil (ou apenas possível) se puderem controlá-lo pelo teclado.

#### Como cumprir - Teclado (2.1.1) {#how-to-meet-keyboard}

Siga as orientações em [Como cumprir o Critério de sucesso 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### Mais informações - Teclado (2.1.1) {#more-information-keyboard}

* [Noções sobre o Critério de sucesso 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Como cumprir o Critério de sucesso 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Nenhuma armadilha de teclado (2.1.2)  {#no-keyboard-trap}

* Critério de Sucesso 2.1.2
* Nível A
* Nenhuma armadilha de teclado: se o foco do teclado puder ser movido para um componente da página usando uma interface do teclado, o foco poderá ser movido para fora desse componente usando apenas uma interface de teclado e, se for necessário mais do que teclas de seta ou tabulação não modificadas ou outros métodos de saída padrão, o usuário será avisado do método para afastar o foco.

#### Propósito - Nenhuma armadilha de teclado (2.1.2) {#purpose-no-keyboard-trap}

O propósito deste Critério de sucesso é garantir que o conteúdo não *trava* o foco do teclado em subseções de conteúdo em uma página da Web. Esse é um problema comum quando vários formatos são combinados em uma página e renderizados usando plug-ins ou aplicativos incorporados.

Pode haver momentos em que a funcionalidade da página da Web restringe o foco a uma subseção do conteúdo (por exemplo, uma caixa de diálogo modal). Nesses casos, você deve fornecer um método para que um usuário possa sair dessa subseção de conteúdo (por exemplo, a tecla ESC fecha a caixa de diálogo modal ou um botão Fechar fecha a caixa de diálogo modal).

#### Como cumprir - Nenhuma armadilha de teclado (2.1.2) {#how-to-meet-no-keyboard-trap}

Siga as orientações em [Como cumprir o Critério de sucesso 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### Mais informações - Nenhuma armadilha de teclado (2.1.2) {#more-information-no-keyboard-trap}

* [Noções sobre o Critério de sucesso 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Como cumprir o Critério de sucesso 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Tempo suficiente (2.2) {#enough-time}

[Diretriz 2.2 de tempo suficiente: forneça aos usuários tempo suficiente para ler e usar o conteúdo.](https://www.w3.org/TR/WCAG/#enough-time)

Isso garante que os usuários tenham tempo suficiente para ler e agir.

### Tempo ajustável (2.2.1)  {#timing-adjustable}

* Critério de Sucesso 2.2.1
* Nível A
* Teclado: forneça aos usuários tempo suficiente para ler e usar o conteúdo.

#### Propósito - Tempo ajustável (2.2.1) {#purpose-timing-adjustable}

O propósito deste Critério de sucesso é garantir que os usuários portadores de deficiência disponham do tempo adequado para interagir com o conteúdo da Web, sempre que possível. Pessoas com deficiências como cegueira, visão baixa, deficiências de destreza e limitações cognitivas podem precisar de mais tempo para ler o conteúdo ou executar funções como preencher formulários on-line. Se as funções da Web dependerem de tempo, será difícil para alguns usuários executar a ação necessária antes que ocorra um limite de tempo. Isso pode tornar o serviço inacessível para eles. Projetar funções que não dependem do tempo ajudará as pessoas com deficiências a concluírem essas funções. Fornecer opções para desativar os limites de tempo, personalizar a duração dos limites de tempo ou solicitar mais tempo antes que um limite ocorra ajuda os usuários que precisam de mais tempo do que o esperado para concluir tarefas com êxito. Essas opções são listadas na ordem que será mais útil para o usuário. Desativar os limites de tempo é melhor do que personalizar a duração dos limites de tempo, o que é melhor do que solicitar mais tempo antes que um limite ocorra.

#### Como cumprir - Tempo ajustável (2.2.1) {#how-to-meet-timing-adjustable}

Siga as orientações em [Como cumprir o Critério de sucesso 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Mais informações - Tempo ajustável (2.2.1) {#more-information-timing-adjustable}

* [Noções sobre o Critério de sucesso 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Como cumprir o Critério de sucesso 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Pausar, Interromper, Ocultar (2.2.2)              {#pause-stop-hide}

* Critério de Sucesso 2.2.2
* Nível A
* Pausar, Interromper, Ocultar: para mover, piscar, deslocar ou atualizar automaticamente as informações, as seguintes opções são verdadeiras:
   * Movimentação, intermitência ou rolagem: para qualquer informação de movimentação, intermitência ou rolagem que
      * a) Inicia automaticamente;
      * b) Tenha uma duração superior a cinco segundos e
      * C) É apresentado em paralelo com outros conteúdos;
existe um mecanismo para o utilizador o pausar, parar ou ocultar, a menos que o movimento, a intermitência ou a deslocação façam parte de uma atividade em que é essencial;
   * Atualização automática: para qualquer informação de atualização automática que
      * a) Inicia automaticamente; e
      * b) É apresentado em paralelo com outros conteúdos
há um mecanismo para o usuário pausar, parar ou ocultar a atualização ou controlar a frequência da atualização, a menos que a atualização automática faça parte de uma atividade em que é essencial.

Os pontos para observar são:

1. Para os requisitos relacionados ao conteúdo piscando ou piscando, consulte Não criar o conteúdo em uma forma conhecida por causar convulsões (2.3).
1. Todo conteúdo da Web deve atender aos critérios de sucesso (independentemente de ser utilizado para atender a outros critérios de sucesso ou não), caso contrário, o usuário pode ser impossibilitado de utilizar a página inteira. Consulte o [Requisito de conformidade 5: não interferência](https://www.w3.org/TR/WCAG20/#cc5).
1. Com relação a um conteúdo que é atualizado periodicamente pelo software ou que é transmitido ao agente do usuário, não é obrigatório armazenar ou apresentar as informações geradas ou recebidas entre o início da pausa e a retomada da apresentação, pois isso pode não ser tecnicamente possível e, em muitas situações, pode gerar informações que não são confiáveis.
1. Em uma fase de pré-carregamento da página, ou um caso similar, na qual a interação não seja possível para todos os usuários, é essencial o uso de uma animação para indicar o progresso do carregamento; caso contrário, o usuário pode pensar que o conteúdo não pôde ser carregado ou que a página travou.

#### Propósito - Pausar, Interromper, Ocultar (2.2.2)       {#purpose-pause-stop-hide}

Alguns usuários podem achar que o conteúdo que se move seja perturbador, ou até mesmo fisicamente doloroso, dificultando a concentração em outras partes da página. Além disso, esse conteúdo pode ser de difícil leitura para os indivíduos que tenham problemas para acompanhar o texto em movimento.

#### Como cumprir - Pausar, Interromper, Ocultar (2.2.2)       {#how-to-meet-pause-stop-hide}

Dependendo da natureza do conteúdo, você pode aplicar uma ou mais das seguintes sugestões ao criar as páginas da Web com um conteúdo em movimento, em modo intermitente ou piscante:

* Forneça um meio de pausar o deslocamento do conteúdo para proporcionar aos usuários tempo suficiente para lê-lo. Por exemplo, marcadores de notícias, texto atualizado automaticamente e carrosséis de imagens que avançam automaticamente.
* Verifique se o conteúdo em modo intermitente é interrompido após cinco segundos.
* Use as tecnologias adequadas para exibir um conteúdo móvel ou intermitente que possa ser desativado pelo navegador. Por exemplo, os arquivos Graphics Interchange Format (GIF) ou Animated Portable Network Graphics (APNG).
* Forneça um controle de formulário na página da Web para permitir que o usuário desative todos os conteúdos móveis ou intermitentes da página.
* Se nenhuma das situações anteriores for possível, forneça um link para uma página que contenha todo o conteúdo móvel ou intermitente.

#### Mais informações - Pausar, Interromper, Ocultar (2.2.2)       {#more-information-pause-stop-hide}

* [Noções sobre o Critério de sucesso 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Como cumprir o Critério de sucesso 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Convulsões e reações físicas (2.3) {#seizures-and-physcial-reactions}

[Diretriz 2.3 de convulsões: não crie o conteúdo em uma forma conhecida por causar convulsões ou reações físicas.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Três flashes ou abaixo do limite (2.3.1)       {#three-flashes-or-below-threshold}

* Critério de Sucesso 2.3.1
* Nível A
* Três flashes ou Abaixo do limite: as páginas da Web não incluem qualquer conteúdo com mais de três flashes no período de um segundo ou o flash encontra-se abaixo dos limites de flash universal e flash vermelho.

>[!NOTE]
>
>Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário em utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte o [Requisito de conformidade 5: não interferência](https://www.w3.org/TR/WCAG/#cc5).

#### Finalidade - Três flashes ou Abaixo do limite (2.3.1) {#purpose-three-flashes-or-below-threshold}

Em certos casos, os flashes podem causar convulsões fotossensíveis. Este é um critério de sucesso para garantir que o usuário tenha acesso a todo o conteúdo sem se preocupar com os flashes.

#### Como cumprir - Três flashes ou Abaixo do limite (2.3.1)       {#how-to-meet-three-flashes-or-below-threshold}

Adote algumas medidas para se certificar de que as seguintes técnicas são aplicadas:

* Garantir que nenhum componente do conteúdo tenha mais de três flashes no período de um segundo;
* Se a condição acima não puder ser cumprida, exibir o conteúdo em modo flash em uma *área pequena de segurança* em pixels na tela. Essa área é calculada usando uma fórmula complexa, abordada em [G176: manter a área de flashes suficientemente pequena](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), de modo que essa técnica só deve ser seguida se o conteúdo de flashes for *necessário.

#### Mais informações - Três flashes ou Abaixo do limite (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Noções sobre o Critério de sucesso 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Como cumprir o Critério de sucesso 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navegável (2.4) {#navigable}

[Diretriz 2.4 Navegável: forneça maneiras de ajudar os usuários a navegar, localizar conteúdo e determinar onde eles estão.](https://www.w3.org/TR/WCAG/#navigable)

Isso garante que o conteúdo seja fácil e direto para os usuários navegarem.

### Ignorar blocos (2.4.1)  {#bypass-blocks}

* Critério de Sucesso 2.4.1
* Nível A
* Ignorar blocos: um mecanismo está disponível para ignorar blocos de conteúdo que são repetidos em várias páginas da Web.

#### Propósito - Ignorar blocos (2.4.1) {#purpose-bypass-blocks}

O propósito deste Critério de sucesso é permitir que as pessoas que navegam sequencialmente pelo conteúdo tenham acesso mais direto ao conteúdo principal da página da Web. Páginas e aplicativos da Web geralmente têm conteúdo que aparece em outras páginas ou telas. Os exemplos de blocos repetidos de conteúdo incluem, entre outros, links de navegação, gráficos de cabeçalho, menus e quadros de publicidade. Pequenas seções repetidas, como palavras individuais, frases ou links únicos não são considerados blocos para os propósitos desta provisão

#### Como cumprir - Ignorar blocos (2.4.1) {#how-to-meet-bypass-blocks}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Mais informações - Ignorar blocos (2.4.1) {#more-information-bypass-blocks}

* [Noções sobre o Critério de sucesso 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Como cumprir o Critério de sucesso 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Página com título (2.4.2)              {#page-titled}

* Critério de Sucesso 2.4.2
* Nível A
* Página com título: as páginas da Web têm títulos que descrevem seu tópico ou finalidade.

#### Finalidade - Página com título (2.4.2)       {#purpose-page-titled}

Esse critério de sucesso ajuda todos, independentemente de quaisquer deficiências, a identificar rapidamente o conteúdo de uma página da Web sem precisar ler a página na íntegra. Isso é útil quando várias páginas da Web estão abertas nas abas do navegador, já que o título da página é exibido na aba e, portanto, pode ser localizado rapidamente.

#### Como cumprir - Página com título (2.4.2)       {#how-to-meet-page-titled}

Quando uma nova página HTML é criada no AEM, é possível especificar o título da página. Certifique-se de que o título descreva adequadamente o conteúdo e o propósito da página, especialmente quaisquer aspectos únicos, para que os visitantes possam identificar rapidamente se o conteúdo é realmente relevante para suas necessidades.

Ao editar uma página, também é possível editar seu título, que pode ser acessado por meio de **Informações da página** - **Propriedades.**

#### Mais informações - Página com título (2.4.2) {#more-information-page-titled}

* [Noções sobre o Critério de sucesso 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Como cumprir o Critério de sucesso 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Ordem de foco (2.4.3)  {#focus-order}

* Critério de Sucesso 2.4.3
* Nível A
* Ordem de foco: se uma página da Web puder ser navegada sequencialmente e as sequências de navegação afetarem o significado ou a operação, os componentes focalizáveis receberão foco em uma ordem que preserve o significado e a operabilidade.

#### Propósito - Ordem de foco (2.4.3) {#purpose-focus-order}

O propósito desse Critério de sucesso é garantir que, quando os usuários navegarem sequencialmente pelo conteúdo, encontrem informações em uma ordem consistente com o significado do conteúdo e que possa ser operada pelo teclado. Isso reduz a confusão ao permitir que os usuários formem um modelo mental consistente do conteúdo. Pode haver diferentes ordens que refletem relações lógicas no conteúdo. Por exemplo, a movimentação pelos componentes em um formulário on-line composto por vários campos e/ou etapas reflete as relações lógicas no conteúdo.

#### Como cumprir - Ordem de foco (2.4.3) {#how-to-meet-focus-order}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Mais informações - Ordem de foco (2.4.3) {#more-information-focus-order}

* [Noções sobre o Critério de sucesso 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Como cumprir o Critério de sucesso 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Finalidade do link (em contexto) (2.4.4)              {#link-purpose-in-context}

* Critério de Sucesso 2.4.4
* Nível A
* Finalidade do link (em contexto): a finalidade de cada link pode ser determinada com base apenas no texto do link ou combinando o texto do link e seu contexto determinado de forma programática, exceto quando a finalidade do link for ambígua para os usuários em geral.

#### Finalidade - Finalidade do link (Em contexto) (2.4.4)       {#purpose-link-purpose-in-context}

Para todos os usuários, independentemente de deficiências, é essencial indicar claramente a direção de um link por meio de um texto de link apropriado. Isso ajuda os usuários a decidir se querem ou não seguir um link. Para usuários deficientes visuais, um texto de link significativo é extremamente útil quando há vários links em uma página (principalmente se a página tiver muito texto), já que textos de link significativos fornecem uma indicação mais clara da funcionalidade da página de destino. Os usuários de algumas tecnologias de assistência, que podem gerar uma lista de todos os links em uma única página, poderão entender mais facilmente o texto do link fora do contexto se o texto do link for exclusivo e informativo. No entanto, pessoas com deficiências cognitivas poderão se confundir se um link não fornecer informações suficientes para descrever com precisão onde o link os levará.

#### Como cumprir - Finalidade do link (Em contexto) (2.4.4)       {#how-to-meet-link-purpose-in-context}

Acima de tudo, verifique se a finalidade de um link está claramente descrita no texto.

* Exemplo incorreto:
   * Texto: para obter mais informações sobre nossas aulas noturnas no segundo trimestre de 2010, clique aqui.
   * Motivo: não indica clara e inequivocamente o seu destino.
* Exemplo correto:
   * Texto: aulas à noite para o segundo trimestre de 2010 - mais informações.
   * Motivo: ajustando ligeiramente o texto e a posição do elemento de link, o texto do link pode ser melhorado:

Os links devem ser redigidos de forma consistente ao longo das páginas, especialmente em barras de navegação. Por exemplo, se um link para uma página específica for chamado de **Publicações** em uma página, use esse texto nas outras páginas para garantir a consistência.

No momento da escrita, há algumas questões relacionadas ao uso de atributos de título para garantir que links semelhantes apresentados em uma página forneçam informações exclusivas sobre o destino (por exemplo, “leia mais” geralmente se refere a vários destinos diferentes):

* O texto contido no atributo de título só está disponível para usuários do mouse como um pop-up de dica de ferramenta e não pode ser acessado de forma consistente usando o teclado ou por usuários móveis.
* Os leitores de tela podem ler atributos de título, mas essa funcionalidade pode não estar habilitada por padrão. Portanto, os usuários podem não estar cientes de que existe um atributo de título.
* É complicado alterar a aparência do texto do título, o que significa que, para algumas pessoas, ele pode ser difícil ou impossível de ler.

Portanto, embora o atributo de título possa ser usado para fornecer contexto adicional a um link, esteja ciente de suas limitações e não o use como alternativa para um texto de link apropriado.

Quando o link for composto de uma imagem, verifique se o texto alternativo para a imagem descreve o destino do link. Por exemplo, se uma imagem de uma estante de livros for definida como um link para as publicações de uma pessoa, o texto alternativo deverá informar **Publicações de John Smith** e não **Estante de livros**.

De maneira alternativa, se a âncora do link contiver um texto que descreva a finalidade do link, além do elemento de imagem (e, portanto, o texto apareça junto com a imagem), use um atributo alternativo vazio para a imagem:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>O trecho acima é uma ilustração; é recomendável usar o componente de **Imagem**.

Embora seja aconselhável fornecer um texto de link que identifique a finalidade do link sem a necessidade de contexto adicional, reconhece-se que isto nem sempre é possível. Link contextuais gratuitos podem ser usados nos casos a seguir, exemplos de HTML que podem ser encontrados em [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* O texto do link faz parte de uma lista de links estritamente relacionados e quando o item de lista que delimita o link fornece contexto suficiente.
* A finalidade de um link pode ser claramente identificada no texto do parágrafo *precedente* (não o seguinte).
* O link está contido em uma tabela de dados e, portanto, a finalidade pode ser claramente identificada nos cabeçalhos associados.
* Uma lista de links está contida em um conjunto de cabeçalhos e o próprio cabeçalho fornece o contexto adequado.
* Há uma lista de links dentro de um link aninhado e o item da lista pai acima do link aninhado fornece o contexto adequado.

Algumas vezes, quando existem vários links em uma página (cada um dos quais fornecendo a direção de um link em detalhes complexos, mas necessários), pode ser apropriado fornecer uma versão alternativa da página da web que mostre exatamente o mesmo conteúdo, mas sem um texto de link tão detalhado.

Como alternativa, use scripts para que uma quantidade mínima de texto seja fornecida no próprio link. Ao ativar um controle apropriado posicionado na parte superior da página, o texto do link é *expandido* para fornecer mais detalhes. Uma abordagem semelhante é usar o CSS para *ocultar* o link completo de usuários deficientes visuais, mas ainda exibi-lo na íntegra para os usuários de leitores de tela. Isso está fora do escopo deste documento, mas mais informações sobre como fazer isso podem ser encontradas na seção [Mais Informações - Finalidade do Link (Em Contexto) (2.4.4)](#more-information-link-purpose-in-context).

#### Mais informações - Finalidade do link (no contexto) (2.4.4) {#more-information-link-purpose-in-context}

* [Noções sobre o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Várias maneiras (2.4.5)  {#multiple-ways}

* Critério de Sucesso 2.4.5
* Nível AA
* Várias maneiras: há mais de uma maneira disponível para localizar uma página da Web em um conjunto de páginas da Web, exceto quando a página da Web é o resultado de um processo ou uma etapa dele.

#### Propósito - Várias maneiras (2.4.5) {#purpose-multiple-ways}

O propósito deste Critério de sucesso é possibilitar que os usuários localizem o conteúdo de uma maneira que melhor atenda as suas necessidades. Os usuários podem achar uma técnica mais fácil ou mais compreensível de usar do que outra.

Mesmo sites pequenos devem fornecer aos usuários alguns meios de orientação. Em um site de três ou quatro páginas, com todas as páginas vinculadas a partir da página inicial, pode ser simplesmente fornecer links de e para a página inicial, onde os links nela também podem servir como um mapa do site.

#### Como cumprir - Várias maneiras (2.4.5) {#how-to-meet-multiple-ways}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### Mais informações - Várias maneiras (2.4.5) {#more-information-multiple-ways}

* [Noções sobre o Critério de sucesso 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Como cumprir o Critério de sucesso 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Títulos e rótulos (2.4.6)  {#headings-and-labels}

* Critério de Sucesso 2.4.6
* Nível AA
* Títulos e rótulos: os títulos e rótulos descrevem o tópico ou o propósito.

#### Propósito - Títulos e rótulos (2.4.6) {#purpose-headings-and-labels}

O propósito deste Critério de sucesso é ajudar os usuários a entenderem quais informações estão contidas em páginas da Web e como essas informações estão organizadas. Quando os títulos são claros e descritivos, os usuários podem encontrar as informações que buscam mais facilmente e podem entender as relações entre diferentes partes do conteúdo com mais facilidade. Os rótulos descritivos ajudam os usuários a identificar componentes específicos dentro do conteúdo.

#### Como cumprir - Títulos e rótulos (2.4.6) {#how-to-meet-headings-and-labels}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### Mais informações - Títulos e rótulos (2.4.6) {#more-information-headings-and-labels}

* [Noções sobre o Critério de sucesso 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Como cumprir o Critério de sucesso 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Foco visível (2.4.7)  {#focus-visible}

* Critério de Sucesso 2.4.7
* Nível AA
* Foco visível: qualquer interface de usuário operável do teclado tem um modo de operação no qual o indicador de foco do teclado está visível.

#### Propósito - Foco visível (2.4.7) {#purpose-focus-visible}

O propósito deste Critério de sucesso é ajudar uma pessoa a saber qual elemento tem o foco do teclado.

Uma pessoa deve ser capaz de saber qual elemento entre vários elementos tem o foco do teclado. Se houver apenas um controle acionável pelo teclado na tela, o critério de sucesso será atendido porque o design visual apresenta apenas um item acionável do teclado.

Quando o critério de sucesso indica “modo de operação”, é com o objetivo de levar em conta as plataformas que nem sempre apresentam um indicador de foco. Normalmente, há apenas um modo de operação, portanto, este critério de sucesso se aplica.

#### Como cumprir - Foco visível (2.4.7) {#how-to-meet-focus-visible}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Mais informações - Foco visível (2.4.7) {#more-information-focus-visible}

* [Noções sobre o Critério de sucesso 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Como cumprir o Critério de sucesso 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Princípio 3: compreensível       {#principle-understandable}

[Princípio 3: compreensível - A informação e a operação da interface do usuário devem ser compreensíveis.](https://www.w3.org/TR/WCAG/#understandable)

### Torne o conteúdo do texto legível e compreensível (3.1)       {#make-text-content-readable-and-understandable}

[Diretriz 3.1 Legível: tornar o conteúdo do texto legível e compreensível.](https://www.w3.org/TR/WCAG/#readable)

### Idioma da página (3.1.1)       {#language-of-page}

* Critério de Sucesso 3.1.1
* Nível A
* Idioma da página: o idioma humano padrão de cada página da Web pode ser determinado de forma programática.

#### Finalidade - Idioma da página (3.1.1)       {#purpose-language-of-page}

A finalidade deste critério de sucesso é garantir que o texto e outros conteúdos linguísticos sejam apresentados corretamente. Para leitores de tela, isso garante que o conteúdo seja pronunciado de forma correta, enquanto os navegadores visuais têm maior probabilidade de exibir determinados conjuntos de caracteres corretamente.

#### Como cumprir - Idioma da página (3.1.1)       {#how-to-meet-language-of-page}

Para cumprir este critério de sucesso, o idioma padrão de uma página da Web pode ser identificado usando o atributo `lang`dentro do elemento`<html>` no topo da página. Por exemplo:

* Se uma página for escrita em inglês, o elemento `<html>` deverá informar:
  `<html lang = "en">`

* Para processar uma página em espanhol, deve ser adotado o seguinte padrão:
  `<html lang = "es">`

No AEM, o idioma padrão da sua página é definido ao criar página, mas também pode ser alterado ao editar as [Propriedades da Página](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>O AEM fornece mais ajustes para variações de um idioma raiz; por exemplo, inglês americano - en-us, inglês britânico - en-gb e inglês canadense - en-ca. Esse nível de detalhes é geralmente supérfluo para a tecnologia de assistência, embora possa ser usado para variações regionais no conteúdo da página.

#### Mais Informações - Idioma da Página (3.1.1) {#more-information-language-of-page}

* [Noções sobre o Critério de sucesso 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Como cumprir o Critério de sucesso 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Os códigos são baseados em ISO 639-1. Uma lista mais extensa de códigos para cada idioma pode ser encontrada no [site W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de Partes (3.1.2)              {#language-of-parts}

* Critério de Sucesso 3.1.2
* Nível AA
* Language of Parts: a linguagem humana de cada passagem ou frase no conteúdo pode ser determinada programaticamente. As exceções são nomes próprios, termos técnicos, palavras de linguagem indeterminada e palavras ou frases que se tornaram parte do vernáculo do texto imediatamente circundante.

#### Finalidade - Idioma de Partes (3.1.2)       {#purpose-language-of-parts}

A finalidade deste critério de sucesso é semelhante ao critério de sucesso de [Idioma da Página](#language-of-page), exceto que se aplica a páginas da Web com conteúdo em múltiplos idiomas em uma única página (por exemplo, devido a citações ou palavras incomuns).

As páginas que utilizam este critério de sucesso permitem:

* O uso do software de transição para o Braille para a inserção de caracteres acentuados.
* Leitores de tela para pronunciar as palavras que têm caracteres especiais ou que não estão no idioma padrão identificado no nível da página.
* Permitem que as ferramentas de tradução, como o Google Translate, traduzam corretamente o conteúdo de um idioma para outro.

#### Como Cumprir - Idioma de Partes (3.1.2)       {#how-to-meet-language-of-parts}

O atributo `lang` pode ser utilizado para identificar alterações no idioma do conteúdo. Por exemplo, uma citação em alemão (ISO 639-1, código “de”) pode ser apresentada da seguinte maneira:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Blocos de citação não são suportados em uma instância predefinida. Um componente personalizado pode ser desenvolvido para oferecer suporte ao recurso.

Da mesma forma, o navegador poderá processar uma palavra incomum ou frase corretamente se o elemento `span` for usado da seguinte maneira:

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Não é necessário seguir este critério de sucesso ao incluir nomes ou cidades em diferentes idiomas. Ou ao usar palavras emprestadas ou frases que se tornaram comuns no idioma padrão, como *schadenfreude* em inglês.

Para adicionar o elemento span, com um idioma apropriado, você pode editar manualmente a sua marcação HTML no modo de edição de fonte da RTE para ser exibido como acima. Como alternativa, o atributo `lang` pode ser incluído na RTE pelo administrador do sistema (consulte [Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Mais Informações - Idioma de Partes (3.1.2) {#more-information-language-of-parts}

* [Noções sobre o Critério de sucesso 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Como cumprir o Critério de sucesso 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Previsível (3.2) {#predictable}

[Diretriz 3.2 Previsível: faça com que as páginas da Web apareçam e operem de maneiras previsíveis.](https://www.w3.org/TR/WCAG/#predictable)

Isso garante que as páginas da Web sejam consistentes na aparência e funcionamento.

### Em foco (3.2.1)  {#on-focus}

* Critério de Sucesso 3.2.1
* Nível A
* Em foco: quando qualquer componente da interface do usuário recebe foco, ele não inicia uma alteração de contexto.

#### Propósito - Em foco (3.2.1) {#purpose-on-focus}

O propósito deste Critério de sucesso é garantir que a funcionalidade seja previsível à medida que os visitantes navegam pelo documento. Qualquer componente que possa acionar um evento quando recebe foco não deve alterar o contexto. Os exemplos de alteração de contexto quando um componente recebe foco incluem, mas não estão limitados a:

* formulários enviados automaticamente quando um componente recebe foco;
* novas janelas abertas quando um componente recebe foco;
* foco alterado para outro componente quando esse componente recebe foco;

O foco pode ser movido para um controle por meio do teclado (por exemplo, tabulação de um controle) ou do mouse (por exemplo, clique em um campo de texto). Mover o mouse sobre um controle não move o foco, a menos que o script implemente esse comportamento. Para alguns tipos de controles, clicar em um controle também pode ativá-lo (por exemplo, botão), que pode, por sua vez, iniciar uma alteração no contexto.

#### Como cumprir - Em foco (3.2.1) {#how-to-meet-on-focus}

Siga as orientações em [Como cumprir o Critério de sucesso 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### Mais informações - Em foco (3.2.1) {#more-information-on-focus}

* [Noções sobre o Critério de sucesso 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Como cumprir o Critério de sucesso 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### Na entrada (3.2.2)  {#on-input}

* Critério de Sucesso 3.2.2
* Nível A
* Na entrada: alterar a configuração de qualquer componente da interface do usuário não causa uma alteração de contexto automaticamente, a menos que o usuário tenha sido avisado do comportamento antes de usar o componente.

#### Propósito - Na entrada (3.2.2) {#purpose-on-input}

O propósito deste Critério de sucesso é garantir que a inserção de dados ou a seleção de um controle de formulário tenha efeitos previsíveis. Alterar a configuração de qualquer componente da interface significa alterar algum aspecto no controle que persistirá quando o usuário não estiver mais interagindo com ele. Portanto, marcar uma caixa de seleção, inserir texto em um campo de texto ou alterar a opção selecionada em um controle de lista altera sua configuração, mas ativar um link ou um botão não altera. As alterações no contexto podem confundir os usuários que não percebem facilmente a mudança ou que são facilmente distraídos por mudanças. As alterações de contexto são apropriadas apenas quando estiver claro que tal alteração ocorrerá em resposta à ação do usuário.

#### Como cumprir - Na entrada (3.2.2) {#how-to-meet-on-input}

Siga as orientações em [Como cumprir o Critério de sucesso 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### Mais informações - Na entrada (3.2.2) {#more-information-on-input}

* [Noções sobre o Critério de sucesso 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Como cumprir o Critério de sucesso 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Navegação consistente (3.2.3)  {#consistent-navigation}

* Critério de Sucesso 3.2.3
* Nível AA
* Navegação consistente: os mecanismos de navegação que são repetidos em várias páginas da Web em um conjunto de páginas ocorrem na mesma ordem relativa sempre que são repetidos, a menos que uma alteração seja iniciada pelo usuário.

#### Propósito - Navegação consistente (3.2.3) {#purpose-consistent-navigation}

O propósito deste Critério de sucesso é incentivar o uso de apresentação e layout consistentes para usuários que interagem com conteúdo repetido em um conjunto de páginas da Web e devem localizar informações ou funcionalidades específicas mais de uma vez. As pessoas com pouca visão que usam ampliação de tela para exibir uma pequena parte da tela por vez geralmente usam dicas visuais e limites de página para localizar rapidamente o conteúdo repetido. Apresentar conteúdo repetido na mesma ordem também é importante para os usuários visuais que usam memória espacial ou dicas visuais no design para localizar conteúdo repetido.

O uso da frase &quot;mesma ordem&quot; nesta seção não significa que os menus de subnavegação não possam ser usados ou que blocos de navegação secundária ou estrutura de página não possam ser usados. Em vez disso, este Critério de sucesso destina-se a ajudar os usuários que interagem com conteúdo repetido em várias páginas da Web a prever a localização do conteúdo que estão procurando. E, para encontrá-lo mais rapidamente quando o encontrarem novamente.

Os usuários podem iniciar uma alteração na ordem ao usar agentes adaptativos do usuário ou definir preferências para que as informações sejam apresentadas de uma forma mais útil para eles.

#### Como cumprir - Navegação consistente (3.2.3) {#how-to-meet-consistent-navigation}

Siga as orientações em [Como cumprir o Critério de sucesso 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### Mais informações - Navegação consistente (3.2.3) {#more-information-consistent-navigation}

* [Noções sobre o Critério de sucesso 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Como cumprir o Critério de sucesso 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Identificação consistente (3.2.4)  {#consistent-identification}

* Critério de Sucesso 3.2.4
* Nível A
* Identificação consistente: os componentes com a mesma funcionalidade em um conjunto de páginas da Web são identificados consistentemente.

#### Propósito - Identificação consistente (3.2.4) {#purpose-consistent-identification}

O propósito deste Critério de sucesso é garantir a identificação consistente de componentes funcionais que aparecem repetidamente em um conjunto de páginas da Web. Uma estratégia que as pessoas que usam leitores de tela usam ao operar um site é contar com a familiaridade com funções que podem aparecer em diferentes páginas da Web. Se funções idênticas tiverem rótulos diferentes (ou, de forma geral, um nome acessível diferente) em diferentes páginas da Web, o site será mais difícil de usar. Pode também ser confuso e aumentar a carga cognitiva de pessoas com limitações cognitivas. Portanto, uma rotulagem consistente ajuda.

Esta coerência abrange as alternativas em texto. Se os ícones ou outros itens não textuais tiverem a mesma funcionalidade, suas alternativas em texto também deverão ser consistentes.

Se houver dois componentes em uma página da Web que tenham a mesma funcionalidade de um componente de outra página em um conjunto de páginas da Web, então todos os 3 devem ser consistentes. Assim, os dois na mesma página serão consistentes.

Embora seja desejável e a prática recomendada sempre ser consistente em uma única página da Web, a 3.2.4 somente aborda a consistência em um conjunto de páginas da Web em que algo é repetido em mais de uma página do conjunto.

#### Como cumprir - Identificação consistente (3.2.4) {#how-to-meet-consistent-identification}

Siga as orientações em [Como cumprir o Critério de sucesso 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### Mais informações - Identificação consistente (3.2.4) {#more-information-consistent-identification}

* [Noções sobre o Critério de sucesso 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Como cumprir o Critério de sucesso 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Assistência de entrada (3.3) {#input-assistance}

[Diretriz 3.3 Assistência de entrada: ajudar os usuários a evitar e corrigir erros](https://www.w3.org/TR/WCAG/#input-assistance)

### Identificação de erro (3.3.1)  {#error-identification}

* Critério de Sucesso 3.3.1
* Nível A
* Identificação do erro: se um erro de entrada for detectado automaticamente, o item com erro é identificado e o erro é descrito ao usuário no texto.

#### Propósito - Identificação de erro (3.3.1) {#purpose-error-identification}

O propósito deste Critério de sucesso é garantir que os usuários estejam cientes de que ocorreu um erro e possam determinar o que está errado. A mensagem de erro deve ser o mais específica possível. Se houver um envio de formulário malsucedido, a reexibição do formulário e a indicação dos campos com erro serão insuficientes para que alguns usuários percebam que ocorreu um erro. Usuários de leitor de tela, por exemplo, não saberão que houve um erro até encontrarem um dos indicadores. Eles podem abandonar o formulário completamente antes de encontrar o indicador de erro, achando que a página simplesmente não está funcionando. De acordo com a definição na WCAG, um [erro de entrada](https://www.w3.org/TR/WCAG/#dfn-input-error) são informações fornecidas pelo usuário que não são aceitas. Isso inclui o seguinte.

Informações exigidas pela página da Web, mas omitidas pelo usuário ou informações fornecidas pelo usuário, mas que não estejam no formato de dados necessário ou valores permitidos.
Por exemplo:

* o usuário não digita a abreviação adequada no campo de estado, província ou região;
* o usuário insere uma abreviação de estado que não é um estado válido;
* o usuário digita um CEP ou código postal inexistente;
* o usuário insere uma data de nascimento de 2 anos no futuro;
* o usuário digita caracteres alfabéticos ou parênteses no campo de número de telefone que só aceita números;
* o usuário insere um lance que está abaixo do lance anterior ou do incremento mínimo de lance.

#### Como cumprir - Identificação de erro (3.3.1) {#how-to-meet-error-identification}

Siga as orientações em [Como cumprir o Critério de sucesso 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### Mais informações - Identificação de erro (3.3.1) {#more-information-error-identification}

* [Noções sobre o Critério de sucesso 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Como cumprir o Critério de sucesso 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Etiquetas ou Instruções (3.3.2)       {#labels-or-instructions}

* Critério de Sucesso 3.3.2
* Nível A
* Rótulos ou instruções: rótulos ou instruções são fornecidos quando o conteúdo exige a entrada do usuário.

#### Finalidade - Etiquetas ou Instruções (3.3.2)       {#purpose-labels-or-instructions}

Fornecer instruções para ajudar as pessoas a preencher formulários é uma parte fundamental das práticas recomendadas de usabilidade da interface. Fazer isso é útil para pessoas com deficiências visuais ou cognitivas, que de outra forma poderiam ter dificuldade para entender o layout de um formulário e o tipo de dados que deve ser fornecido em um campo de formulário específico.

##### Forms

No projeto de demonstração WKND do AEM, um rótulo padrão é adicionado quando você adiciona um componente de formulário, como um **Campo de texto**, à página. O título padrão depende do tipo de componente. Você pode adicionar seu próprio título na guia **Título e texto** da caixa de diálogo de edição desse campo. É importante garantir que as etiquetas ajudem os usuários a compreender os dados associados a cada componente do formulário.

O campo de **Título** deve ser usado para elementos de campo, pois ele fornece um rótulo que é disponibilizado para a tecnologia de acessibilidade. Apenas escrever um rótulo no texto ao lado do campo não é suficiente.

Para alguns componentes de formulário, também é possível ocultar visualmente as etiquetas usando a caixa de seleção **Ocultar título**. As etiquetas ocultas dessa maneira ainda estarão disponíveis para a tecnologia assistiva, mas não serão exibidas na tela. Embora essa possa ser uma boa abordagem em algumas situações, é melhor incluir um rótulo visual sempre que possível, pois alguns usuários podem estar olhando para uma pequena seção da tela (um campo de cada vez) e precisam dos rótulos para identificar o campo corretamente.

###### Botões de imagem {#image-buttons}

Quando são usados botões de imagem (por exemplo, o componente **Botão de Imagem** do projeto WKND), o campo **Título** da guia **Título e Texto** da caixa de diálogo de edição fornece o texto alternativo para a imagem, em vez do rótulo. Assim, no exemplo abaixo, a imagem com o texto `Submit`tem o texto alternativo de `Submit`, adicionado usando o campo **Título** na janela de edição.

###### Grupos de campos de formulário {#groups-of-form-fields}

No projeto WKND, quando houver um grupo de controles relacionados, como um **Grupo de opções**, talvez seja necessário fornecer um título para o grupo, bem como controles individuais. Ao adicionar um conjunto de botões de opção no AEM, o campo **Título** fornece esse título de grupo, enquanto títulos individuais são especificados conforme os botões de opção (**Itens**) são criados.

Contudo, não existe uma associação programática entre o título do grupo e os próprios botões de opção. Os editores de modelo devem envolver o título nas marcas `fieldset` e `legend` necessárias para criar esta associação e isso só pode ser feito através da edição do código fonte da página. Alternativamente, um administrador do sistema pode adicionar suporte a esses elementos para que eles apareçam na janela **Propriedades do Campo** (consulte [Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

###### Considerações adicionais para formulários {#additional-considerations-for-forms}

Se os dados devem ser inseridos em um formato específico, deixe isso claro no texto da etiqueta. Por exemplo, se uma data deve ser inscrita no formato `DD-MM-YYYY`, indique isso especificamente como parte da etiqueta. Isso significa que quando os usuários de leitores de tela encontrarem o campo, o rótulo será anunciado automaticamente, junto com as informações adicionais sobre o formato.

Se a entrada de um campo de formulário for obrigatória, deixe isso claro usando a palavra &quot;obrigatório&quot; como parte do rótulo. O AEM adiciona um asterisco quando um campo é obrigatório, mas seria ideal incluir a palavra `required` na própria etiqueta (no campo **Título** na janela de edição).

O posicionamento dos rótulos também é importante, pois ajuda a localizar os campos apropriados. Isso é particularmente importante quando o usuário se depara com um formulário complexo. Siga as orientações abaixo:

* As caixas de seleção ou botões de opção:
As etiquetas são posicionadas imediatamente à direita do campo.
* Todos os outros componentes do formulário (por exemplo, caixas de texto, caixas de combinação):
os rótulos são posicionados imediatamente acima ou à esquerda do campo.

Em formulários simples com funcionalidade limitada, a identificação adequada de um botão `Submit` pode servir como etiqueta para o campo adjacente (por exemplo, `Search`). Isso é útil em situações em que encontrar espaço para o texto da etiqueta pode ser difícil.

#### Mais Informações - Etiquetas ou Instruções (3.3.2)       {#more-information-labels-or-instructions}

* [Noções sobre o Critério de sucesso 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Como cumprir o Critério de sucesso 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Sugestão de erro (3.3.3)  {#error-suggestion}

* Critério de Sucesso 3.3.3
* Nível AA
* Teclado: se um erro de entrada for detectado automaticamente e as sugestões para correção forem conhecidas, as sugestões serão fornecidas ao usuário, a menos que isso comprometa a segurança ou o propósito do conteúdo.

#### Propósito - Sugestão de erro (3.3.3) {#purpose-error-suggestion}

O propósito deste Critério de sucesso é garantir que os usuários recebam sugestões adequadas para a correção de um erro de entrada, se possível. A definição de [erro de entrada](https://www.w3.org/TR/WCAG/#dfn-input-error) da WCAG diz &quot;informações fornecidas pelo usuário que não são aceitas&quot; pelo sistema. Alguns exemplos de informações que não são aceitas incluem informações obrigatórias, mas omitidas pelo usuário, e informações fornecidas pelo usuário, mas que não estão no formato de dados necessário ou valores permitidos.

O Critério de sucesso 3.3.1 prevê a notificação de erros. Mas as pessoas com limitações cognitivas podem ter dificuldade para entender como corrigir os erros. Pessoas com deficiências visuais podem não ser capazes de descobrir exatamente como corrigir o erro. Se o envio do formulário não for bem-sucedido, os usuários poderão abandonar o formulário por não ter certeza de como corrigir o erro, mesmo sabendo que ele ocorreu.

O autor do conteúdo pode fornecer a descrição do erro, ou o agente do usuário pode fornecer a descrição do erro com base em informações específicas da tecnologia, determinadas de forma programática.

#### Como cumprir - Sugestão de erro (3.3.3) {#how-to-meet-error-suggestion}

Siga as orientações em [Como cumprir o Critério de sucesso 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### Mais informações - Sugestão de erro (3.3.3) {#more-information-error-suggestion}

* [Noções sobre o Critério de sucesso 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Como cumprir o Critério de sucesso 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Prevenção de erros (legal, financeiro, dados) (3.3.4)  {#error-prevention-legal-financial-data}

* Critério de Sucesso 3.3.4
* Nível AA
* Prevenção de erros (legal, financeiro, dados): em páginas da Web que façam com que compromissos legais ou transações financeiras ocorram para o usuário, que modifiquem ou excluam dados controláveis pelo usuário em sistemas de armazenamento de dados, ou que enviem respostas de teste do usuário, pelo menos um dos seguintes é verdadeiro:

   * Reversível
Os envios são reversíveis.
   * Verificados
É dada uma oportunidade de corrigir os dados digitados pelo usuário que são verificados em busca de erros de entrada.
   * Confirmado
Um mecanismo está disponível para revisar, confirmar e corrigir informações antes de finalizar o envio.

#### Propósito - Prevenção de erros (legal, financeiro, dados) (3.3.4) {#purpose-error-prevention-legal-financial-data}

O propósito deste Critério de sucesso é ajudar os usuários portadores de deficiências a evitarem consequências graves como resultado de um erro ao executar uma ação que não pode ser revertida. Por exemplo, a compra de passagens não reembolsáveis ou a apresentação de uma ordem de compra de ações numa conta de corretagem são transações financeiras com graves consequências. Se um usuário tiver cometido um engano sobre a data da viagem aérea, ele poderá terminar com uma passagem com o dia errado que não pode ser trocada. Se o usuário tiver cometido um erro no número de ações a serem compradas, poderia acabar comprando mais ações do que o esperado. Ambos os tipos de erros dispendiosos envolvem transações que ocorrem imediatamente e não podem ser alteradas posteriormente. Da mesma forma, pode ser um erro irrecuperável se os usuários modificarem ou excluírem involuntariamente os dados armazenados em um banco de dados que precisarão acessar posteriormente, como todo o perfil de viagem em um site de serviços de viagens. No que se refere à modificação ou exclusão de dados &#39;controláveis pelo usuário&#39;, a intenção é evitar a perda em massa de dados, como a exclusão de um arquivo ou registro. Não é a intenção exigir uma confirmação de cada comando save ou a simples criação ou edição de documentos, registros ou outros dados.

Os usuários portadores de deficiências podem ter mais probabilidade de cometer erros. As pessoas com deficiências de leitura podem transpor números e letras, e aquelas com deficiências motoras podem apertar as teclas por engano. Fornecer a capacidade de reverter ações permite que os usuários corrijam um erro que pode resultar em consequências graves. Fornecer a capacidade de revisar e corrigir informações dá ao usuário a oportunidade de detectar um erro antes de tomar uma ação que tenha consequências graves.

Os dados controláveis pelo usuário são dados visualizáveis pelo usuário que ele pode alterar e/ou excluir por meio de uma ação intencional. Os exemplos de usuários que controlam esses dados seriam a atualização do número de telefone e do endereço da conta do usuário ou a exclusão de um registro de faturas anteriores de um site. Ele não se refere a coisas como registros da Internet e dados de monitoramento de mecanismo de pesquisa com os quais o usuário não pode visualizar ou interagir diretamente.

#### Como cumprir - Prevenção de erros (legal, financeiro, dados) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Siga as orientações em [Como cumprir o Critério de sucesso 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Mais informações - Prevenção de erros (legal, financeiro, dados) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Noções sobre o Critério de sucesso 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Como cumprir o Critério de sucesso 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Princípio 4: Robusto {#principle-robust}

[Princípio 4: robusto - o conteúdo deve ser robusto o suficiente para que possa ser interpretado por uma grande variedade de agentes de usuário, incluindo tecnologias assistivas.](https://www.w3.org/TR/WCAG/#robust)

### Compatível (4.1) {#compatible}

[Compatível com a diretriz 4.1: aumente a compatibilidade com os agentes do usuário atuais e futuros, incluindo as tecnologias assistivas.](https://www.w3.org/TR/WCAG/#compatible)

Aumente a compatibilidade com os agentes do usuário atuais e futuros, incluindo as tecnologias assistivas.

### Análise (4.1.1)  {#parsing}

* Critério de Sucesso 4.1.1
* Nível A
* Análise: no conteúdo implementado que usa idiomas de marcação, os elementos têm tags de início e fim completas, os elementos são aninhados de acordo com as especificações, os elementos não contêm atributos duplicados e as IDs são exclusivas, exceto quando as especificações permitem esses recursos.

#### Propósito - Análise (4.1.1) {#purpose-parsing}

O propósito deste Critério de sucesso é garantir que os agentes do usuário, incluindo as tecnologias assistivas, possam interpretar e analisar o conteúdo com precisão. Se o conteúdo não puder ser analisado em uma estrutura de dados, agentes de usuário diferentes poderão apresentá-lo de forma diferente ou não poderão analisá-lo. Alguns agentes do usuário usam &quot;técnicas de reparo&quot; para renderizar conteúdo mal codificado.

Como as técnicas de reparo variam entre os agentes do usuário, os autores não podem assumir que o conteúdo é analisado com precisão em uma estrutura de dados ou que será renderizado corretamente por agentes do usuário especializados, incluindo tecnologias assistivas, a menos que o conteúdo seja criado de acordo com as regras definidas na gramática formal dessa tecnologia. Em idiomas de marcação, erros na sintaxe do elemento e no não fornecimento de tags de início/fim aninhadas corretamente levam a erros que impedem os agentes do usuário de analisar o conteúdo de forma confiável. Portanto, o Critério de sucesso exige que o conteúdo possa ser analisado usando apenas as regras da gramática formal.

#### Como cumprir - Análise (4.1.1) {#how-to-meet-parsing}

Siga as orientações em [Como cumprir o Critério de sucesso 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Mais informações - Análise (4.1.1) {#more-information-parsing}

* [Noções sobre o Critério de sucesso 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Como cumprir o Critério de sucesso 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nome, função, valor (4.1.2)  {#name-role-value}

* Critério de Sucesso 4.1.2
* Nível A
* Nome, Função, Valor: para todos os componentes da interface (incluindo, mas não limitados a: elementos de formulário, links e componentes gerados por scripts), o nome e a função podem ser determinados de forma programática; estados, propriedades e valores que podem ser definidos pelo usuário podem ser definidos de forma programática; e a notificação de alterações nesses itens está disponível aos agentes de usuário, incluindo tecnologias assistivas.

#### Propósito - Nome, Função, Valor (4.1.2) {#purpose-ame-role-value}

O propósito deste Critério de sucesso é garantir que as Tecnologias assistivas (AT) possam coletar informações sobre, ativar ou definir e manter-se atualizadas sobre o status dos controles da interface do usuário no conteúdo.

Quando controles padrão de tecnologias assistivas são usados, esse processo é simples. Se os elementos da interface forem usados de acordo com as especificações, as condições desta provisão serão atendidas. (Veja os exemplos do Critério de sucesso 4.1.2 abaixo)

No entanto, se os controles personalizados forem criados ou se os elementos de interface forem programados (em código ou script) para terem uma função e/ou função diferente da usual, medidas adicionais deverão ser tomadas para garantir que os controles forneçam informações importantes para as tecnologias assistivas e permitam que eles sejam controlados por tecnologias assistivas.

Um estado particularmente importante de um controle da interface é se ele tem ou não foco. O estado de foco de um controle pode ser determinado de forma programática e as notificações sobre mudança de foco são enviadas aos agentes do usuário e à tecnologia de assistência. Outros exemplos de estado de controle da interface do usuário são se uma caixa de seleção ou um botão de opção foi selecionado. Ou se um nó de árvore ou de lista que pode ser recolhido é expandido ou recolhido.

#### Como cumprir - Nome, Função, Valor (4.1.2) {#how-to-meet-ame-role-value}

Siga as orientações em [Como cumprir o Critério de sucesso 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Mais informações - Nome, função, valor (4.1.2 {#more-information-ame-role-value}

* [Noções sobre o Critério de sucesso 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Como cumprir o Critério de sucesso 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
