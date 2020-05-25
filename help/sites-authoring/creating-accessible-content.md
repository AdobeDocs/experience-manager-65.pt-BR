---
title: Criação de conteúdo acessível para o Adobe Experience Manager (Conformidade com WCAG 2.1)
description: Use o AEM para ajudar a tornar o conteúdo da Web acessível e utilizável por pessoas com deficiências
translation-type: tm+mt
source-git-commit: cb7df7301364eb1ce3a1ca376256d2cd5afcb2c8
workflow-type: tm+mt
source-wordcount: '13956'
ht-degree: 98%

---


# Criação de conteúdo acessível (Conformidade com o WCAG 2.1) {#creating-accessible-content-wcag-conformance}

As [Diretrizes de acessibilidade de conteúdo da Web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), elaboradas por [um grupo de trabalho do World Wide Wec Consortium](https://www.w3.org/Consortium/activities#Accessibility_Guidelines_Working_Group), consistem em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável por pessoas com deficiência.

Como introdução, o consórcio fornece uma série de seções e documentos de apoio:

* [Novos recursos na WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Como cumprir a WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Noções básicas sobre a WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Técnicas da WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Os documentos da WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Além disso, consulte:
* Nosso [Guia rápido para a WCAG 2.1](/help/managing/qg-wcag.md).
* Os [Relatórios de conformidade para acessibilidade de soluções da Adobe](https://www.adobe.com/accessibility/compliance.html).
* [Configuração do Editor de Rich Text para produzir conteúdo acessível](/help/sites-administering/rte-accessible-content.md)

As diretrizes são classificadas de acordo com os três níveis de conformidade: Nível A (o mais baixo), Nível AA e Nível AAA (o mais alto). Resumidamente, os níveis são definidos como apresentado a seguir:

* **Nível A**: o site atinge um nível mínimo básico de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A são cumpridos.
* **Nível AA:** esse é um nível ideal de acessibilidade que você deve almejar, no qual seu site atinge um nível fundamental de acessibilidade, de forma a ser acessível para a maioria das pessoas na maior parte das situações usando a maioria das tecnologias. Para atingir esse nível, todos os Critérios de sucesso do Nível A e Nível AA são cumpridos.
* **Nível AAA**: o site atinge um nível muito alto de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A, Nível AA e Nível AAA são cumpridos.

Ao criar o seu site, é necessário determinar o nível global com o qual você gostaria que ele estivesse em conformidade.

A seção a seguir apresenta as [camadas das Diretrizes da WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) com os critérios de sucesso relacionados aos [níveis de conformidade](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A e AA.

>[!NOTE]
>
>Nesse documento são usados:
>
>* [Os nomes curtos das Diretrizes da WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* [A numeração usada nas Diretrizes da WCAG 2.1](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) para auxiliar na referência cruzada com o site da WCAG.


## Princípio 1: perceptível      {#principle-perceivable}

[Princípio 1: perceptível - As informações e os componentes da interface do usuário têm de ser apresentados aos usuários de formas perceptíveis.](https://www.w3.org/TR/WCAG/#perceivable)

### Alternativas em texto (1.1)      {#text-alternatives}

[Diretriz 1.1 Alternativas em texto: fornecer alternativas em texto para qualquer conteúdo não textual, para que seja possível alterá-lo para outras formas mais adequadas à necessidade do indivíduo, como impressão em caracteres ampliados, braille, fala, símbolos ou linguagem mais simples.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Conteúdo não textual (1.1.1)      {#non-text-content}

* Critério de Sucesso 1.1.1
* Nível A
* Conteúdo não textual: todo o conteúdo não textual que é apresentado ao usuário tem uma alternativa em texto que serve um propósito equivalente, exceto para as situações indicadas abaixo.

#### Finalidade - Conteúdo não textual (1.1.1) {#purpose-non-text-content}

As informações em uma página da Web podem ser fornecidas em vários formatos não textuais diferentes, como imagens, vídeos, animações, gráficos e tabelas. Os indivíduos cegos ou com deficiências visuais graves não conseguem visualizar o conteúdo não textual, mas podem acessar o conteúdo textual através da leitura por um leitor de tela ou apresentado na forma tátil por um dispositivo de exibição em Braille. Portanto, ao disponibilizar alternativas em texto para o conteúdo no formato gráfico, os indivíduos que não conseguem visualizá-lo podem acessar uma versão equivalente das informações disponibilizadas.

Um benefício adicional útil é que as alternativas em texto permitem que o conteúdo não textual seja indexado pela tecnologia do mecanismo de pesquisa.

#### Como cumprir - Conteúdo não textual (1.1.1)      {#how-to-meet-non-text-content}

Para gráficos estáticos, o requisito básico é o de proporcionar uma alternativa em texto equivalente para o gráfico. Isso pode ser feito no campo Texto **** alternativo; consulte, por exemplo, a **[Imagem](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/components/image.html)**do componente principal.

>[!NOTE]
>
>Alguns Componentes principais predefinidos, como o **[Carrossel](https://docs.adobe.com/content/help/pt/experience-manager-core-components/using/components/carousel.html)**, não fornecem um campo de Texto****alternativo para adicionar descrições de texto alternativo a imagens individuais, embora exista o campo**Rótulo **(guia**[Acessibilidade](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** ) para o componente inteiro.
>
>Ao implementar as versões desses componentes para a instância do AEM, sua equipe de desenvolvimento precisará configurá-los para suportar o atributo `alt`[, para que os autores possam adicioná-lo ao conteúdo (consulte Adicionar suporte para elementos HTML e atributos adicionais](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

Por padrão, o AEM requer que o campo **Texto alternativo** seja preenchido. Se a imagem for meramente decorativa e um texto alternativo não for necessário, será possível marcar a opção **A imagem é decorativa**.

#### Criar boas alternativas de texto {#creating-good-text-alternatives}

Existem várias formas de conteúdo não textual, de modo que o valor da alternativa em texto dependerá da função que o gráfico vai desempenhar na página da Web. Algumas regras gerais que devem ser seguidas incluem:

* As alternativas em texto devem ser breves, mas devem capturar claramente as informações essenciais fornecidas pelo conteúdo não textual.
* Descrições excessivamente longas (mais de 100 caracteres) devem ser evitadas. Se um texto alternativo exigir mais detalhes:
   * forneça uma breve descrição no texto alternativo
   * e tiver uma descrição mais longa no texto em outro lugar na mesma página ou em uma página separada. Vincule para essa descrição separada, tornando a imagem um link ou colocando um link de texto adjacente à imagem.
* O texto alternativo não deve replicar o conteúdo fornecido no formulário de texto próximo à mesma página. Lembre-se que muitas imagens são ilustrações de pontos já abordados no texto de uma página, então é possível que já exista uma alternativa detalhada em texto.
* Se o conteúdo não textual for um link para outra página ou documento e não houver nenhum outro texto que faça parte do mesmo link, então o texto alternativo da imagem deve indicar o destino do link e não descrever a imagem.
* Se o conteúdo não textual estiver em um elemento de botão e não houver nenhum texto que faça parte do mesmo botão, então o texto alternativo da imagem deve indicar a funcionalidade do botão e não descrever a imagem.
* É perfeitamente aceitável disponibilizar para uma imagem um texto alternativo vazio (nulo), mas apenas se ela não precisar de um texto alternativo (por exemplo, ela é um gráfico meramente decorativo) ou se o texto equivalente já existir no texto da página.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Tipos específicos de conteúdo não textual que necessitam de alternativas em texto podem incluir:

* Fotos ilustrativas:
São imagens de pessoas, objetos ou lugares. É importante pensar na função da foto na página e, em geral, é recomendável descrever o conteúdo da imagem, já que a tecnologia de assistência anunciará o tipo de elemento (por exemplo, `graphic` ou `image`). Pode aumentar a clareza usar `screenshot` ou `illustration` nas descrições de texto alternativo, mas isso depende do contexto. A consistência é um fator importante. Uma decisão deve ser tomada para toda a equipe de criação, e isso deve ser aplicado à toda a experiência do usuário.
* Ícones:
São pequenos pictogramas (gráficos) que transmitem informações específicas. Eles devem ser usados de forma consistente em uma página e um site. Todas as instâncias do ícone em uma página ou um site devem ter a mesma alternativa em texto curta e sucinta, a menos que isso resulte em duplicação desnecessária do texto adjacente.
* Tabelas e gráficos: geralmente representam dados numéricos. Dessa forma, uma opção para fornecer uma alternativa em texto pode ser incluir um breve resumo das principais tendências indicadas na tabela ou gráfico. Se necessário, também forneça uma descrição mais detalhada no texto usando o campo **Descrição** na guia de propriedades de imagem **Avançadas**. Além disso, você pode fornecer os dados de origem em forma de tabela em outro lugar na página ou no site.
* Mapas, diagramas, fluxogramas: para gráficos que fornecem dados espaciais (por exemplo, para suportar a descrição das relações entre objetos ou um processo), verifique se a mensagem principal é fornecida em formato de texto e se essa informação sobre o texto está posicionada perto de cada ponto de dados associado. Em mapas, fornecer um equivalente de texto completo provavelmente não será prático, mas se o mapa for fornecido como uma forma de ajudar as pessoas a encontrar o caminho para um determinado local, o texto alternativo da imagem do mapa poderá indicar brevemente o *Mapa de X* e, em seguida, fornecer direções para esse local no texto em outro lugar na página ou por meio do campo **Descrição** na guia **Avançado** do componente **Imagem**.
* CAPTCHAs:
Um CAPTCHA é um *teste de Turing público completamente automatizado para diferenciação entre computadores e humanos*. É uma verificação de segurança usada em páginas da Web para diferenciar os humanos de um software mal-intencionado, mas que pode causar barreiras de acessibilidade. São imagens que exigem que os usuários descrevam o que visualizam, a fim de passar por um teste de segurança. Fornecer uma alternativa em texto para a imagem, obviamente, não é possível, portanto, em vez disso, você terá de considerar as soluções alternativas não gráficas.
O W3C fornece uma série de sugestões, como: cada uma dessas abordagens tem suas próprias vantagens e desvantagens.
   * Enigmas de lógica
   * O uso da saída de som, em vez de imagens
   * Contas e filtros de spam de uso limitado.
* Imagens de plano de fundo: são obtidas usando a Cascading Style Sheets (CSS), em vez de HTML. Isso significa que não é possível especificar um valor de texto alternativo. Portanto, as imagens de plano de fundo não devem fornecer informações textuais importantes - se o fizerem, também devem ser disponibilizadas no texto da página. No entanto, é importante que um plano de fundo alternativo seja mostrado quando a imagem não puder ser exibida.

>[!NOTE]
>
>Deve haver um nível adequado de contraste entre o plano de fundo e o texto de primeiro plano; isso é abordado com mais detalhes na seção [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Mais informações - Conteúdo não contextual (1.1.1)      {#more-information-non-text-content}

* [Noções sobre o Critério de sucesso 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Como cumprir o Critério de sucesso 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Explicação do W3C sobre as alternativas para CAPTCHAs](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Mídia com base no tempo (1.2)      {#time-based-media}

[Diretriz de mídia com base no tempo 1.2: fornece alternativas para a mídia com base no tempo.](https://www.w3.org/TR/WCAG/#time-based-media)

Trata-se de um conteúdo da Web que é *baseado no tempo*. Isso abrange o conteúdo que o usuário pode reproduzir (como vídeo, áudio e conteúdo animado) e pode ser pré-gravado ou ter transmissão ao vivo.

### Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Critério de sucesso 1.2.1
* Nível A
* Apenas áudio e apenas vídeo (pré-gravado): para mídia somente de áudio e somente de vídeo pré-gravada, as informações a seguir são verdadeiras, exceto quando o áudio ou vídeo for uma alternativa em mídia para o texto e claramente identificada como tal:
   * Apenas áudio pré-gravado: uma alternativa para a mídia com base no tempo é fornecida, que apresenta informações equivalentes para o conteúdo composto apenas de áudio pré-gravado.
   * Apenas vídeo pré-gravado: é fornecida uma faixa de áudio ou uma alternativa para a mídia com base no tempo, que apresenta informações equivalentes para o conteúdo composto apenas de vídeo pré-gravado.

#### Propósito - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Problemas de acessibilidade para vídeo e áudio podem ser enfrentados por:

* Pessoas com deficiência visual, quando não há trilha sonora ou a mesma não é suficiente para informá-los sobre o que está acontecendo no vídeo ou animação;
* Pessoas com deficiências auditivas ou surdas, que não podem ouvir a trilha sonora;
* Pessoas que podem ouvir a trilha sonora, mas não entendem o que está sendo falado (por exemplo, porque está em um idioma que não entendem).

O vídeo ou áudio também pode estar disponível para as pessoas que utilizam navegadores ou dispositivos que não suportam a reprodução de conteúdo em formatos de mídia específicos, como o Adobe Flash.

Fornecer essas informações em um formato diferente, como texto (ou áudio para vídeo sem áudio), pode torná-lo acessível às pessoas que não conseguem acessar o conteúdo original.

#### Como cumprir - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Se o conteúdo for um áudio pré-gravado sem vídeo (como um podcast):
   * Forneça um link imediatamente antes ou depois do conteúdo para obter uma transcrição do texto do conteúdo de áudio.
A transcrição deve ser uma página HTML com um equivalente em texto de todo o conteúdo falado e não-falado importante, além de uma indicação de quem está falando, uma descrição do cenário, expressões vocais e uma descrição de qualquer outro áudio significativo.
* Se o conteúdo for uma animação ou vídeo pré-gravado sem áudio:
   * Forneça um link imediatamente antes ou depois do conteúdo para uma descrição de texto equivalente das informações fornecidas pelo vídeo
   * Ou uma descrição de áudio equivalente em um formato de áudio normalmente utilizado, como MP3.

>[!NOTE]
>
>Se o conteúdo de áudio ou vídeo for fornecido como uma alternativa ao conteúdo que já existe em outro formato na mesma página da Web, talvez não seja necessária uma alternativa adicional.
>
>As orientações em [Entenda a WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html) fornecem mais informações.

Inserir multimídia em suas páginas da Web do AEM é semelhante à inserção de uma imagem. No entanto, como o conteúdo multimídia é muito maior do que uma imagem estática, há diversas configurações e opções para controlar a forma como a multimídia é reproduzida.

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

Use as legendas ocultas sempre que possível, já que proporcionam ao usuário a escolha de visualizar ou não as legendas. 

Para as legendas ocultas, será necessário criar e fornecer um arquivo de legenda sincronizada em um formato adequado (como [SMIL](https://www.w3.org/AudioVideo/)), junto com o arquivo de vídeo (os detalhes sobre como proceder estão fora do escopo desse guia, mas fornecemos links para alguns tutoriais em [Mais informações - Legendas (pré-gravadas) (1.2.2)](#more-information-captions-prerecorded). Certifique-se de fornecer uma nota ou ativar o recurso de legenda no player de vídeo para informar aos usuários que legendas estão disponíveis para o vídeo.

Se você precisar usar as legendas abertas, insira o texto na faixa de vídeo. Essa ação pode ser realizada utilizando aplicativos de edição de vídeo que permitem a sobreposição de títulos no vídeo.

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
* Descrição de áudio ou alternativa de mídia (pré-gravada): é fornecida uma descrição de áudio ou uma alternativa para mídia com base no tempo do conteúdo de vídeo pré-gravado para a mídia sincronizada, exceto quando a mídia for uma alternativa para texto e claramente identificada como tal. 

#### Propósito - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Os indivíduos que são cegos ou deficientes visuais vão enfrentar barreiras de acessibilidade se as informações em um vídeo ou uma animação forem fornecidas apenas visualmente, ou se a trilha sonora não fornecer informações suficientes para permitir a compreensão do que está acontecendo visualmente.

#### Como cumprir - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Existem duas abordagens que podem ser adotadas para atender a esse critério de sucesso. Ambas são aceitáveis:

1. Incluir uma descrição de áudio adicional para o conteúdo do vídeo. Isso pode ser feito de uma das três maneiras:
   * Durante as pausas no diálogo existente, forneça informações sobre as mudanças na cena que não são apresentadas como parte da faixa de áudio atual;
   * Forneça uma faixa de áudio nova, adicional e opcional contendo a trilha sonora original, mas incluindo também informações de áudio extras sobre as mudanças no cenário.
      * Isso permite que os usuários alternem entre a faixa de áudio existente (que *não* contém uma descrição de áudio) e a nova faixa de áudio (que *contém* uma descrição de áudio).
      * Isso evita a interrupção para os usuários que não precisam de descrição adicional.
   * Crie uma segunda versão do conteúdo de vídeo para permitir descrições de áudio estendidas. Isso reduz as dificuldades associadas à disponibilização de descrições de áudio detalhadas em lacunas entre o diálogo existente, pausando temporariamente o áudio e o vídeo em pontos adequados. Como resultado, uma descrição de áudio muito maior pode ser disponibilizada, antes que a ação inicie novamente. Como no exemplo anterior, essa é a melhor opção fornecida como uma faixa de áudio extra opcional, a fim de evitar a interrupção para os usuários que não precisam de uma descrição adicional.
1. Fornecer uma transcrição de texto que seja um equivalente de texto adequado dos elementos visuais e de áudio do vídeo ou animação. Isso deve incluir, conforme o caso, uma indicação de quem está falando, uma descrição do cenário, quaisquer eventos ou informações apresentados visualmente e expressões vocais. Dependendo da extensão, você pode colocar a transcrição na mesma página que o vídeo ou a animação, ou em uma página separada; caso escolha a última opção, forneça um link para a transcrição ao lado do vídeo ou da animação.

Detalhes exatos de como criar um vídeo descrito por áudio estão fora do escopo desse guia. A criação de descrições de vídeo e áudio pode ser demorada, mas outros produtos da Adobe podem ajudar a realizar essas tarefas.

#### Mais informações - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Noções sobre o Critério de sucesso 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Como cumprir o Critério de sucesso 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Legendas (ao vivo) (1.2.4)            {#captions-live}

* Critério de sucesso 1.2.4
* Nível AA
* Legendas (ao vivo): são fornecidas legendas para todo o conteúdo de áudio ao vivo na mídia sincronizada.

#### Propósito - Legendas (ao vivo) (1.2.4)      {#purpose-captions-live}

Esse critério de sucesso é idêntico às [Legendas (pré-gravadas)](#captions-prerecorded), já que aborda as barreiras de acessibilidade enfrentadas pelos indivíduos surdos ou com deficiências auditivas, exceto que esse critério de sucesso lida com as apresentações ao vivo, como webcasts.

#### Como cumprir - Legendas (ao vivo) (1.2.4) {#how-to-meet-captions-live}

Siga as orientações fornecidas para as [Legendas (pré-gravadas)](#captions-prerecorded) acima. No entanto, como a mídia é ao vivo, a disposição da legenda tem de ser criada o mais rápido possível e em resposta ao que está acontecendo. Portanto, você deve considerar o uso de legendagem em tempo real ou ferramentas de voz para texto.

Instruções detalhadas estão além do escopo desse documento, mas os seguintes recursos disponibilizam informações úteis:

* [WebAIM: legendagem em tempo real](https://www.webaim.org/techniques/captions/realtime.php)

* [Projeto AccessComputing (University of Washington): as legendas podem ser geradas automaticamente usando reconhecimento de voz?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### Mais informações - Legendas (ao vivo) (1.2.4)      {#more-information-captions-live}

* [Noções sobre o Critério de sucesso 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Como cumprir o Critério de sucesso 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Descrição de áudio (pré-gravado) (1.2.5)  {#audio-description-prerecorded}

* Critério de Sucesso 1.2.5
* Nível AA
* Descrição de áudio (pré-gravado): é fornecida uma descrição de áudio para todos os conteúdos de vídeo pré-gravados em uma mídia sincronizada.

#### Propósito - Descrição de áudio (pré-gravado) (1.2.5) {#purpose-audio-description-prerecorded}

Esse critério de sucesso é idêntico à [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-prerecorded), exceto que os autores devem fornecer uma descrição de áudio muito mais detalhada para estar em conformidade com o Nível AA.

#### Como cumprir - Descrição de áudio (pré-gravado) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Siga as orientações fornecidas para a [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-prerecorded).

#### Mais informações - Descrição de áudio (pré-gravado) (1.2.5) {#more-information-audio-description-prerecorded}

* [Noções sobre o Critério de sucesso 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Como cumprir o Critério de sucesso 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptável (1.3)      {#adaptable}

[Diretriz adaptável 1.3: criar conteúdos que possam ser apresentados de diferentes formas (por exemplo, um layout mais simples) sem perder as informações ou a estrutura.](https://www.w3.org/TR/WCAG/#adaptable)

Essa diretriz abrange os requisitos necessários para auxiliar os indivíduos que:

* pode não ser capaz de acessar as informações apresentadas por um autor na apresentação padrão desse conteúdo (por exemplo, um layout de várias colunas ou uma página com uso intenso de cores e/ou imagens).

* usam uma exibição visual alternativa ou apenas de áudio, como um texto grande ou contraste alto.

### Informações e Relações (1.3.1)            {#info-and-relationships}

* Critério de Sucesso 1.3.1
* Nível A
* Informações e Relações: as informações, a estrutura e as relações transmitidas através de apresentação podem ser determinadas de forma programática ou disponíveis no texto.

#### Propósito - Informações e Relações (1.3.1)      {#purpose-info-and-relationships}

Muitas tecnologias de assistência utilizadas por indivíduos com deficiência contam com informações estruturais, a fim de exibir ou *compreender* o conteúdo de forma eficiente. Essas informações estruturais podem assumir a forma de cabeçalhos de página, linha de tabela e cabeçalhos de coluna e tipos de lista. Por exemplo, um leitor de tela pode permitir que um usuário navegue por uma página de um cabeçalho a outro. No entanto, quando o conteúdo da página parece ter a estrutura somente por meio de um estilo visual, em vez do HTML subjacente, então não há informações estruturais disponíveis para as tecnologias de assistência, o que limita a sua capacidade para auxiliar a navegação mais fácil.

Esse critério de sucesso existe para garantir que a informação estrutural seja fornecida programaticamente via HTML, ou outras técnicas de codificação, de modo que os navegadores e as tecnologias de assistência possam acessar e aproveitar as informações.

#### Como cumprir - Informações e Relações (1.3.1)      {#how-to-meet-info-and-relationships}

O AEM facilita a construção de conteúdo da Web semanticamente significativo usando os elementos HTML apropriados. Abra o conteúdo da página no RTE (um componente de Texto) e use o menu **Formatar parágrafo** (símbolo de parágrafo) para especificar o elemento estrutural adequado (por exemplo, parágrafo, cabeçalho etc.).

É possível verificar se as suas páginas da Web têm a estrutura adequada, usando os seguintes elementos, quando aplicável:

* **Cabeçalhos:** desde que você tenha os recursos de acessibilidade do RTE ativados, o AEM oferece três níveis de cabeçalho de página. É possível usá-los para identificar seções e subseções de conteúdo. O cabeçalho 1 é o nível mais alto, o Cabeçalho 3 o mais baixo. O administrador do sistema pode configurar o sistema para permitir o uso de mais níveis de cabeçalho.

* **Listas**: você pode usar HTML para especificar três tipos diferentes de listas:
   * O elemento `<ul>` é usado para listas *desordenadas* (com marcadores). Os itens da lista individual são identificados usando o elemento `<li>`. No RTE, use o ícone **Lista de marcadores**.
   * O elemento `<ol>` é usado para as listas *numeradas*. Os itens da lista individual são identificados usando o elemento `<li>`. No RTE, use o ícone **Lista numerada** .
   Caso deseje alterar o conteúdo existente em um tipo de lista específica, destaque o texto e selecione o tipo de lista adequado. Como no exemplo anterior, que mostra como o texto do parágrafo é inserido, os elementos desejados da lista são adicionados automaticamente ao seu HTML.

   No modo de tela cheia, os ícones **Lista com marcadores** e **Lista numerada** ficam visíveis. Quando não estiver no modo de tela cheia, as duas opções estarão disponíveis no ícone **Listas**.

* **Tabelas**: Tabelas de dados devem ser identificadas usando os elementos da tabela de HTML:
   * um elemento `<table>`
   * um elemento `<tr>` para cada linha da tabela
   * um elemento `<th>` para cada linha e cabeçalho da coluna
   * um elemento `<td>` para cada célula de dados
   Além disso, as tabelas acessíveis usam os seguintes elementos e atributos:

   * O elemento `<caption>` é usado para fornecer uma legenda visível para a tabela. As legendas por padrão são exibidas de forma centralizada acima da tabela, mas podem ser posicionadas adequadamente usando o CSS. A legenda é associada à tabela de forma programada, portanto, é um método útil para fornecer uma introdução ao conteúdo.
   * O elemento `<summary>` auxilia os usuários com deficiências visuais a compreender de forma mais fácil as informações apresentadas em uma tabela, fornecendo um resumo do que pode ser visto. Isso é particularmente útil quando layouts complexos ou não convencionais são usados (esse atributo não é exibido no navegador, somente é lido nas tecnologias de assistência).
   * O `scope` atributo do elemento `<th>` é usado para indicar se uma célula representa um cabeçalho de uma linha ou de uma coluna específica. Uma abordagem semelhante é a de usar o cabeçalho e os atributos de id em tabelas complexas, onde as células de dados podem ser associadas a um ou mais cabeçalhos.
   >[!NOTE]
   >
   >Por padrão, esses elementos e atributos não estão diretamente disponíveis, embora o administrador do sistema possa adicionar o suporte para esses valores na caixa de diálogo **Propriedades da tabela**[ (consulte Adicionar suporte para outros elementos e atributos de HTML](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes).

   Para abrir a caixa de diálogo **Tabela** onde é possível selecionar a guia **Propriedades da tabela**:

   * Defina uma **legenda** apropriada.
   * Remova qualquer valor padrão para **Largura**, **Altura**, **Borda**, **Preenchimento da célula e** **Espaçamento entre células**. já que essas propriedades podem ser definidas em uma planilha de estilos global.
   Em seguida, você pode usar as **Propriedades da célula** para escolher se a célula é uma célula de dados ou de cabeçalho:

* **Ênfase**: Use o elemento `<strong>` ou `<em>` para indicar ênfase. Não use os cabeçalhos para destacar o texto dentro dos parágrafos.
   * Destaque o texto que deseja enfatizar;
   * Clique no ícone **B** (para `<strong>`) ou **I** (para `<em>`) exibidos no painel **Propriedades** (verifique se o HTML está selecionado).

      >[!NOTE]
      >
      >O RTE em uma instalação padrão do AEM está configurado para usar:
      >
      >* `<b>` para `<strong>`
      >* `<i>` para `<em>`
      >
      >Eles são efetivamente os mesmos, mas `<strong>` e `<em>` são preferíveis, pois são html semanticamente corretos. Sua equipe de desenvolvimento pode configurar o RTE para usar `<strong>` e `<em>` (em vez de `<b>` e `<i>`), ao desenvolver a instância do projeto.


* **Tabelas de dados complexos**: em alguns casos, onde há tabelas complexas com dois ou mais níveis de cabeçalhos, as Propriedades da tabela básicas podem não ser suficientes para fornecer toda a informação estrutural necessária. Para esses tipos de tabelas complexas, relações diretas precisam ser criadas entre os cabeçalhos e as suas células relacionadas usando os atributos **cabeçalho** e **id**.

   >[!NOTE]
   >
   >O atributo id não está disponível em uma instalação predefinida. Ele pode ser ativado através da configuração de regras de HTML e do serializador no RTE.

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

   Para obter isso no AEM você deve adicionar a marcação diretamente, usando o modo de edição da fonte.

   >[!NOTE]
   >
   >Essa funcionalidade não está disponível imediatamente em uma instalação padrão. Ela exige uma configuração de RTE; regras de HTML e serializador.

#### Mais informações - Informações e Relações (1.3.1) {#more-information-info-and-relationships}

* [Noções sobre o Critério de sucesso 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Como cumprir o Critério de sucesso 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Sequência significativa (1.3.2)  {#meaningful-sequence}

* Critério de Sucesso 1.3.2
* Nível A
* Sequência significativa: quando a sequência na qual o conteúdo é apresentado afeta seu significado, uma sequência de leitura correta pode ser determinada programaticamente.

#### Propósito - Sequência significativa (1.3.2) {#purpose-meaningful-sequence}

O propósito deste Critério de sucesso é permitir que um agente do usuário forneça uma apresentação alternativa do conteúdo, preservando a ordem de leitura necessária para entender o significado. É importante que seja possível determinar programaticamente pelo menos uma sequência do conteúdo que faça sentido. O conteúdo que não atende a esse Critério de sucesso pode confundir ou desorientar os usuários quando a tecnologia assistiva ler o conteúdo na ordem errada, ou quando são aplicadas planilhas de estilos alternativas ou outras alterações de formatação.

#### Como cumprir - Sequência significativa (1.3.2) {#how-to-meet-meaningful-sequence}

Siga as orientações em [Como cumprir o Critério de sucesso 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Mais informações - Sequência significativa (1.3.2) {#more-information-meaningful-sequence}

* [Noções sobre o Critério de sucesso 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Como cumprir o Critério de sucesso 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Características sensoriais (1.3.3)            {#sensory-characteristics}

* Critério de Sucesso 1.3.3
* Nível A
* Características sensoriais: as instruções fornecidas para compreender e utilizar o conteúdo não dependem somente das características sensoriais dos componentes, como forma, tamanho, localização visual, orientação ou som.

#### Propósito - Características sensoriais (1.3.3)      {#purpose-sensory-characteristics}

Os designers muitas vezes se concentram nos recursos de design visual, como cor, forma, estilo de texto ou uma parte da posição absoluta ou relativa do conteúdo ao apresentar as informações. Estas podem ser técnicas de design muito poderosas na transmissão de informações (e podem melhorar a acessibilidade geral para usuários com necessidades de acessibilidade cognitiva), mas pessoas cegas ou deficientes visuais podem não conseguir acessar informações que exigem a identificação visual de atributos como posição, cor ou forma.

Da mesma forma, as informações que exigem a distinção entre sons diferentes (por exemplo, o conteúdo falado masculino ou feminino) vão apresentar barreiras de acessibilidade para os indivíduos com deficiência auditiva, se não estiverem refletidas em nenhuma alternativa em texto para o conteúdo de áudio.

>[!NOTE]
>
>Para os requisitos relacionados às alternativas de cor, consulte [Uso de cor](#use-of-color).

#### Como cumprir - Características sensoriais (1.3.3)      {#how-to-meet-sensory-characteristics}

Certifique-se de que todas as informações baseadas em características visuais do conteúdo da página também são apresentadas em um formato alternativo.

* Não se baseie na posição visual para fornecer informações. Por exemplo, se você deseja fazer uma referência para os usuários sobre um menu no lado direito da página para obter acesso a mais informações, não se refira ao *menu à direita*; em vez disso, nomeie o menu (por exemplo, através de um cabeçalho) e faça uma referência a esse nome no texto. 
* Não se baseie no estilo do texto (por exemplo, negrito ou itálico) como a única maneira de transmitir as informações.

>[!NOTE]
>
>A utilização dos termos descritivos será aceitável se estes forem entendidos como relevantes em um contexto não visual. Por exemplo, normalmente é aceitável o uso dos termos *acima* e *abaixo,* já que sugerem, respectivamente, um conteúdo antes e depois de um item específico; isso ainda faria sentido com o conteúdo falado em voz alta.

#### Mais informações - Características sensoriais (1.3.3)      {#more-information-sensory-characteristics}

* [Noções sobre o Critério de sucesso 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Como cumprir o Critério de sucesso 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Discernível (1.4)      {#distinguishable}

[Diretriz 1.4 Discernível: facilitar a visualização e a audição de conteúdos aos usuários, incluindo a separação do primeiro plano e do plano de fundo. ](https://www.w3.org/TR/WCAG/#distinguishable)

### Utilização de cor (1.4.1)            {#use-of-color}

* Critério de Sucesso 1.4.1
* Nível A
* Utilização de cor: a cor não é utilizada como o único meio visual de transmitir informações, indicar uma ação, solicitar uma resposta ou distinguir um elemento visual.

>[!NOTE]
>
>Esse critério de sucesso aborda especificamente a percepção da cor. Outras formas de percepção são abordadas na seção [Adaptável (1.3)](#adaptable); incluindo o acesso programático à cor e outras codificações de apresentação visual.

#### Propósito - Utilização de cor (1.4.1)      {#purpose-use-of-color}

A cor é, obviamente, uma forma eficaz de melhorar o apelo estético das páginas da Web e também é útil na transmissão de informações. No entanto, há uma série de deficiências visuais, da cegueira ao daltonismo, o que significa que algumas pessoas não conseguem distinguir entre certas cores. disponibilizar informações. 

Por exemplo, um indivíduo com daltonismo não conseguirá distinguir entre tons de verde e vermelho. É possível que ele veja as cores como uma terceira cor (por exemplo, marrom), nesse caso, o indivíduo não conseguirá distinguir entre o vermelho, verde e marrom.

Além disso, a cor pode não ser percebida por indivíduos que usam navegadores somente de texto, dispositivos com visor monocromático ou que exibem uma impressão em preto e branco da página.

Uma outra consideração é o estado *selecionado* de um elemento de interface (por exemplo, guias, botões de alternância, entre outros), que precisa ser transmitido de alguma forma que não seja apenas com cor e além de apenas uma apresentação visual. Para esses elementos, o uso adicional de padrões, formas e informações programáticas é útil ao criar uma experiência do usuário totalmente inclusiva que não depende de um sentido específico.

#### Como cumprir - Utilização de cor (1.4.1)      {#how-to-meet-use-of-color}

Sempre que a cor for usada para transmitir informações, certifique-se de que a informação está disponível, sem a necessidade da visualização das cores.

Por exemplo, verifique se as informações fornecidas através das cores também estão evidentes no texto.

Se a cor for usada como dica para fornecer informações, você deve fornecer uma dica visual adicional, como a alteração do estilo (por exemplo, negrito, itálico) ou da fonte. Isso ajuda as pessoas com pouca visão ou daltonismo a identificar as informações. No entanto, não é possível depender dessas opções completamente, uma vez que isso não ajudará os indivíduos que não conseguem visualizar nada na página. Portanto, é (às vezes) útil fornecer texto oculto ou usar soluções programáticas, como o [pacote de padrões da Web ARIA (Accessible Rich Internet Applications)](https://www.w3.org/WAI/standards-guidelines/aria/), para transmitir essas informações a usuários sem visão.

#### Mais informações - Utilização de cor (1.4.1) {#more-information-use-of-color}

* [Noções sobre o Critério de sucesso 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Como cumprir o Critério de sucesso 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Controle de áudio (1.4.2)  {#audio-control}

* Critério de Sucesso 1.4.2
* Nível A
* Controle de áudio: se qualquer áudio em uma página da Web for reproduzido automaticamente por mais de 3 segundos, um mecanismo estará disponível para pausar ou parar o áudio, ou um mecanismo estará disponível para controlar o volume de áudio independentemente do nível geral de volume do sistema.

#### Propósito - Controle de áudio (1.4.2) {#purpose-audio-control}

Os indivíduos que usam software de leitura de tela podem achar difícil ouvir a saída da fala se houver outra reprodução de áudio ao mesmo tempo. Essa dificuldade é exacerbada quando a saída de voz do leitor de tela é baseada em software (como a maioria é hoje) e é controlada pelo mesmo controle de volume do som. Além disso, algumas pessoas com deficiências cognitivas e neurodivergentes podem ter sensibilidade ao som. Essas pessoas considerarão qualquer incapacidade de alterar o nível do volume do conteúdo de áudio bastante perturbadora.

Portanto, é importante que o usuário possa desligar o som de fundo.

>[!NOTE]
>
>Ter controle do volume inclui a capacidade de reduzir seu volume para zero.

#### Como cumprir - Controle de áudio (1.4.2) {#how-to-meet-audio-control}

Siga as orientações em [Como cumprir o Critério de sucesso 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Mais informações - Controle de áudio (1.4.2) {#more-information-audio-control}

* [Noções sobre o Critério de sucesso 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Como cumprir o Critério de sucesso 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contraste (Mínimo) (1.4.3)      {#contrast-minimum}

* Critério de Sucesso 1.4.3
* Nível AA
* Contraste (Mínimo): a apresentação visual e as imagens do texto têm uma relação de contraste de, no mínimo, 4.5:1, exceto para o seguinte:
   * Texto ampliado: o texto ampliado e as imagens compostas por texto ampliado têm uma relação de contraste de, no mínimo, 3:1.
   * Incidental: o texto ou as imagens de texto que fazem parte de um componente de interface de usuário inativo, que são [meramente decorativos](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), e não estão visíveis para ninguém ou que são parte de uma imagem que inclui outro conteúdo visual significativo, não têm requisito de contraste.
   * Logotipos: o texto que faz parte de um logotipo ou marca comercial não tem requisito de contraste.
   >[!NOTE]
   >
   >See [Understanding Non-text Contrast](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) for further information, to help ensure that content authors understand the additional requirements around non-text elements (including icons, interface elements, amongst others).

#### Propósito - Contraste (Mínimo) (1.4.3)      {#purpose-contrast-minimum}

Os indivíduos com certas deficiências visuais podem não conseguir distinguir entre determinados pares de cores com baixo contraste. Problemas de acessibilidade podem ocorrer para esses indivíduos, se:

*  O texto contrasta mal com a cor de fundo.
* A codificação de cores do texto (como o texto do link e texto comum) for importante para diferenciar as informações.

>[!NOTE]
>
>O texto usado exclusivamente para fins decorativos está excluído desse critério de sucesso.

#### Como cumprir - Contraste (Mínimo) (1.4.3)      {#how-to-meet-contrast-minimum}

Verifique se o texto contrasta o suficiente com o plano de fundo. As relações de contraste dependem do tamanho e do estilo do texto em questão:

* Para texto com menos de 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste entre o texto/imagens de texto e o plano de fundo deve ser, pelo menos, 4.5:1.
* Para o texto com até 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste deve ser de pelo menos 3:1.
* Se um plano de fundo for estampado, então ele deve ser sombreado ao redor do texto, de modo que a relação 4.5:1 ou 3:1 seja mantida.

>[!NOTE]
>
>Lembre-se de que as fontes podem diferir na forma como renderizam o tamanho equivalente de PT/PX/EM.
>
>Recomenda-se usar bom senso e pecar a favor da legibilidade e da usabilidade ao selecionar as fontes e o dimensionamento apropriados para o conteúdo da Web.

>[!NOTE]
>
>Os seguintes sites podem ajudar com conversões para outras unidades:
>
>* [Px to Em Calculater - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [Font size conversion: pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com: PX to EM conversion made simple](http://pxtoem.com)


Para verificar as relações de contraste, use uma ferramenta de contraste em cores, como o [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) ou o [verificador de contraste em cores do WebAIM](https://www.webaim.org/resources/contrastchecker/). Essas ferramentas permitem que você verifique os pares de cores e informe quaisquer problemas de contraste.

De forma alternativa, se você estiver menos preocupado sobre como especificar a aparência de sua página, é possível optar por não especificar as cores do texto de plano de fundo e de primeiro plano. Nenhuma verificação de contraste é necessária, já que o navegador do usuário determinará as cores do texto e plano de fundo.

Se não for possível atender aos níveis de contraste recomendados, será necessário fornecer um link para uma versão alternativa equivalente da página (que não tenha problemas de contraste de cor), ou permitir que o usuário ajuste o contraste do esquema de cores da página de acordo com as suas próprias necessidades.

#### Mais informações - Contraste (Mínimo) (1.4.3)      {#more-information-contrast-minimum}

* [Noções sobre o Critério de sucesso 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Como cumprir o Critério de sucesso 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Redimensionar texto (1.4.4)  {#resize-text}

* Critério de Sucesso 1.4.4
* Nível A
* Redimensionar texto: exceto em legendas e imagens de texto, o texto pode ser redimensionado sem tecnologia assistiva até 200% sem perda de conteúdo ou funcionalidade.

#### Propósito - Redimensionar texto (1.4.4) {#purpose-resize-text}

O propósito deste Critério de sucesso é garantir que o texto renderizado visualmente, incluindo controles baseados em texto (caracteres de texto que foram exibidos para que possam ser vistos [vs. caracteres de texto que ainda estejam na forma de dados como ASCII]) possam ser dimensionados com sucesso para que sejam lidos diretamente por pessoas com deficiências visuais leves, sem a necessidade do uso de tecnologia de assistência, como um ampliador de tela. Os usuários podem se beneficiar do dimensionamento de todo o conteúdo na página da Web, mas o texto é mais importante.

#### Como cumprir - Redimensionar texto (1.4.4) {#how-to-meet-resize-text}

Além de seguir as diretrizes em [Como atender ao critério para o sucesso 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text), você pode incentivar os autores de conteúdo a usar larguras e alturas fluidas e flexíveis em seus designs de página e tamanhos de fonte (por exemplo, web design responsivo) para permitir que os leitores possam redimensionar o texto.

#### Mais informações - Redimensionar texto (1.4.4) {#more-information-resize-text}

* [Noções sobre o Critério de sucesso 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Como cumprir o Critério de sucesso 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Imagens de texto (1.4.5)      {#images-of-text}

* Critério de Sucesso 1.4.5
* Nível AA
* Imagens de texto: se as tecnologias usadas puderem obter a apresentação visual, o texto será usado para transmitir as informações, em vez das imagens de texto, exceto para o seguinte:
   * Personalizável: a imagem do texto pode ser visualmente personalizada para as necessidades do usuário;
   * Básico: uma apresentação específica do texto é fundamental para a transmissão das informações.

>[!NOTE]
>
>Os logotipos (texto que faz parte de um logotipo ou marca comercial) são considerados fundamentais.

#### Propósito - Imagens de texto (1.4.5)      {#purpose-images-of-text}

As imagens de texto são usadas, frequentemente, quando um estilo de texto específico é o preferido; por exemplo, um logotipo ou se o texto foi gerado de uma outra fonte (por exemplo, uma verificação de um documento em papel). No entanto, em comparação com o texto apresentado em HTML e o estilo usando CSS, as imagens de texto não têm flexibilidade para mudar o tamanho ou aparência, o que pode ser necessário para os indivíduos com deficiência visual ou dificuldade de leitura.

#### Como cumprir - Imagens de texto (1.4.5)      {#how-to-meet-images-of-text}

Se as imagens de texto tiverem que ser utilizadas, use o CSS para substituir as imagens de texto pelo texto equivalente em HTML, para que o texto seja disponibilizado de forma personalizada. Para ver um exemplo, consulte o [C30: usar o CSS para substituir o texto por imagens de texto e fornecer controles de interface do usuário para fazer a alteração](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Mais informações - Imagens de texto (1.4.5)      {#more-information-images-of-text}

* [Noções sobre o Critério de sucesso 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Como cumprir o Critério de sucesso 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Princípio 2: operável      {#principle-operable}

[Princípio 2: operável - os componentes da interface de usuário e a navegação precisam ser operáveis.](https://www.w3.org/TR/WCAG/#operable)

### Acessível por teclado (2.1) {#keyboard-accessible}

[Diretriz 2.1 acessível por teclado: disponibilize toda a funcionalidade de um teclado.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Isso garante que os usuários possam acessar toda a funcionalidade usando um teclado.

### Teclado (2.1.1)  {#keyboard}

* Critério de Sucesso 2.1.1
* Nível A
* Teclado: toda a funcionalidade do conteúdo é operável por meio de uma interface de teclado sem exigir tempos específicos para pressionamentos de teclas individuais, exceto quando a função subjacente requer uma entrada que depende do caminho do movimento do usuário, não apenas dos pontos finais.

#### Propósito - Teclado (2.1.1) {#purpose-keyboard}

O objetivo desse Critério de sucesso é garantir que, sempre que possível, o conteúdo possa ser operado por meio de um teclado ou a interface de teclado (para que um teclado alternativo possa ser usado). Quando o conteúdo pode ser operado por meio de um teclado ou teclado alternativo, ele pode ser operado por pessoas sem visão (que não podem usar dispositivos como mouse que exige coordenação ocular), bem como por pessoas que precisam usar teclados alternativos ou dispositivos de entrada que atuam como emuladores de teclado. Os emuladores de teclado incluem software de entrada de fala, software sip-and-puff, teclados na tela, software de digitalização e uma variedade de tecnologias assistiva e teclados alternativos. Os indivíduos com pouca visão também podem ter problemas para rastrear um ponteiro e achar o uso do software muito mais fácil (ou apenas possível) se puderem controlá-lo pelo teclado.

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

O propósito deste Critério de sucesso é garantir que os usuários portadores de deficiência disponham do tempo adequado para interagir com o conteúdo da Web, sempre que possível. Pessoas com deficiências como cegueira, visão baixa, deficiências de destreza e limitações cognitivas podem precisar de mais tempo para ler o conteúdo ou executar funções como preencher formulários online. Se as funções da Web dependerem de tempo, será difícil para alguns usuários executar a ação necessária antes que ocorra um limite de tempo. Isso pode tornar o serviço inacessível para eles. Projetar funções que não dependem do tempo ajudará as pessoas com deficiências a concluírem essas funções. Fornecer opções para desativar os limites de tempo, personalizar a duração dos limites de tempo ou solicitar mais tempo antes de ocorrer um limite de tempo ajuda os usuários que precisam de mais tempo do que o esperado para concluírem com êxito as tarefas. Essas opções são listadas na ordem que será mais útil para o usuário. Desativar os limites de tempo é melhor do que personalizar a duração dos limites de tempo, o que é melhor do que solicitar mais tempo antes que um limite ocorra.

#### Como cumprir - Tempo ajustável (2.2.1) {#how-to-meet-timing-adjustable}

Siga as orientações em [Como cumprir o Critério de sucesso 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Mais informações - Tempo ajustável (2.2.1) {#more-information-timing-adjustable}

* [Noções sobre o Critério de sucesso 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Como cumprir o Critério de sucesso 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Pausar, Interromper, Ocultar (2.2.2)            {#pause-stop-hide}

* Critério de Sucesso 2.2.2
* Nível A
* Pausar, Interromper, Ocultar: para mover, piscar, deslocar ou atualizar automaticamente as informações, as seguintes opções são verdadeiras:
   * Mover, piscar, deslocar: para qualquer movimento, modo intermitente ou deslocamento, que (a) é iniciado automaticamente, (b) dura mais de cinco segundos e (c) seja apresentado em paralelo com outro conteúdo, existe um mecanismo para o usuário pausar, interromper ou ocultar, a menos que o movimento, o modo intermitente ou o deslocamento seja parte fundamental de uma atividade;
   * Atualizar automaticamente: para atualizar automaticamente qualquer informação que (a) é iniciada automaticamente e (b) seja apresentada em paralelo com outro conteúdo, existe um mecanismo para o usuário pausar, interromper ou ocultar, ou para controlar a frequência da atualização, a menos que a opção para atualizar automaticamente seja parte fundamental de uma atividade.

Os pontos para observar são:

1. Para os requisitos relacionados ao conteúdo no modo intermitente ou piscante, consulte Não criar o conteúdo em uma forma conhecida por causar convulsões (2.3).
1. Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário em utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte o [Requisito de conformidade 5: não interferência](https://www.w3.org/TR/WCAG20/#cc5).
1. O conteúdo que é atualizado periodicamente pelo software ou que é transmitido para o agente de usuário, não é obrigado a preservar ou apresentar as informações geradas ou recebidas entre o início da pausa e a retomada da apresentação, pois isso pode não ser tecnicamente possível e, em muitas situações, pode induzir ao erro. 
1. Uma animação que ocorre como parte de uma fase de pré-carregamento ou uma situação similar pode ser considerada essencial se a interação não puder ocorrer durante essa fase para todos os usuários, e se não indicar o progresso, poderá confundir os usuários ou levá-los a pensar que o conteúdo foi congelado ou interrompido.

#### Propósito - Pausar, Interromper, Ocultar (2.2.2)      {#purpose-pause-stop-hide}

Alguns usuários podem achar que o conteúdo que se move é perturbador, ou até mesmo fisicamente doloroso, dificultando a concentração em outras partes da página. Além disso, esse conteúdo pode ser de difícil leitura para os indivíduos que têm problemas para acompanhar o texto em movimento.

#### Como cumprir - Pausar, Interromper, Ocultar (2.2.2)      {#how-to-meet-pause-stop-hide}

Dependendo da natureza do conteúdo, você pode aplicar uma ou mais das seguintes sugestões ao criar as páginas da Web com um conteúdo em movimento, em modo intermitente ou piscante:

* Forneça um meio de pausar o deslocamento do conteúdo para proporcionar aos usuários tempo suficiente para lê-lo. Por exemplo, marcadores de notícias, texto atualizado automaticamente e carrosséis de imagens que avançam automaticamente.
* Verifique se o conteúdo em modo intermitente é interrompido após cinco segundos.
* Use as tecnologias adequadas para exibir um conteúdo móvel ou intermitente que possa ser desativado pelo navegador. Por exemplo, os arquivos Graphics Interchange Format (GIF) ou Animated Portable Network Graphics (APNG).
* Forneça um controle de formulário na página da Web para permitir que o usuário desative todos os conteúdos móveis ou intermitentes da página.
* Se nenhuma das situações anteriores for possível, forneça um link para uma página que contenha todo o conteúdo móvel ou intermitente.

#### Mais informações - Pausar, Interromper, Ocultar (2.2.2)      {#more-information-pause-stop-hide}

* [Noções sobre o Critério de sucesso 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Como cumprir o Critério de sucesso 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Convulsões e reações físicas (2.3) {#seizures-and-physcial-reactions}

[Diretriz 2.3 de convulsões: não crie o conteúdo em uma forma conhecida por causar convulsões ou reações físicas.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Três flashes ou abaixo do limite (2.3.1)      {#three-flashes-or-below-threshold}

* Critério de Sucesso 2.3.1
* Nível A
* Três flashes ou Abaixo do limite: as páginas da Web não incluem qualquer conteúdo com mais de três flashes no período de um segundo ou o flash encontra-se abaixo dos limites de flash universal e flash vermelho.

>[!NOTE]
>
>Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário em utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte o [Requisito de conformidade 5: não interferência](https://www.w3.org/TR/WCAG/#cc5).

#### Finalidade - Três flashes ou Abaixo do limite (2.3.1) {#purpose-three-flashes-or-below-threshold}

Em certos casos, os flashes podem causar convulsões fotossensíveis. Este critério de sucesso permite aos usuários acessar e utilizar todo o conteúdo sem se preocupar com o conteúdo com flashes.

#### Como cumprir - Três flashes ou Abaixo do limite (2.3.1)      {#how-to-meet-three-flashes-or-below-threshold}

É necessário adotar algumas medidas para se certificar de que as seguintes técnicas são aplicadas:

* Garantir que nenhum componente do conteúdo tenha mais de três flashes no período de um segundo;
* Se a condição acima não puder ser cumprida, exibir o conteúdo em modo flash em uma *área pequena de segurança* em pixels na tela. Essa área é calculada utilizando uma fórmula complexa, abordada em [G176: manter a área de flashes suficientemente pequena](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), de modo que essa técnica só deve ser seguida se o conteúdo em modo flash for *absolutamente* necessário.

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

O propósito deste Critério de sucesso é permitir que as pessoas que navegam sequencialmente pelo conteúdo tenham acesso mais direto ao conteúdo principal da página da Web. Páginas e aplicativos da Web geralmente têm conteúdo que aparece em outras páginas ou telas. Os exemplos de blocos repetidos de conteúdo incluem, entre outros, links de navegação, gráficos de cabeçalho, menus e quadros de publicidade. Para efeitos desta disposição, não se consideram blocos pequenas seções repetidas, como palavras individuais, frases ou links únicos.

#### Como cumprir - Ignorar blocos (2.4.1) {#how-to-meet-bypass-blocks}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Mais informações - Ignorar blocos (2.4.1) {#more-information-bypass-blocks}

* [Noções sobre o Critério de sucesso 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Como cumprir o Critério de sucesso 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Página com título (2.4.2)            {#page-titled}

* Critério de Sucesso 2.4.2
* Nível A
* Página com título: as páginas da Web têm títulos que descrevem o tópico ou a finalidade.

#### Finalidade - Página com título (2.4.2)      {#purpose-page-titled}

Este critério de sucesso ajuda as pessoas, independentemente de qualquer incapacidade cognitiva, a identificar o conteúdo de uma página da Web sem precisar ler toda a página. Isso é especialmente útil quando várias páginas da Web estão abertas em abas de navegador, já que o título da página é exibido na aba e, portanto, pode ser localizado rapidamente.

#### Como cumprir - Página com título (2.4.2)      {#how-to-meet-page-titled}

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

O propósito desse Critério de sucesso é garantir que, quando os usuários navegarem sequencialmente pelo conteúdo, encontrem informações em uma ordem consistente com o significado do conteúdo e que possa ser operada pelo teclado. Isso reduz a confusão ao permitir que os usuários formem um modelo mental consistente do conteúdo. Pode haver diferentes ordens que refletem relações lógicas no conteúdo. Por exemplo, a movimentação pelos componentes em um formulário online composto por vários campos e/ou etapas reflete as relações lógicas no conteúdo.

#### Como cumprir - Ordem de foco (2.4.3) {#how-to-meet-focus-order}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Mais informações - Ordem de foco (2.4.3) {#more-information-focus-order}

* [Noções sobre o Critério de sucesso 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Como cumprir o Critério de sucesso 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Finalidade do link (em contexto) (2.4.4)            {#link-purpose-in-context}

* Critério de Sucesso 2.4.4
* Nível A
* Finalidade do link (em contexto): a finalidade de cada link pode ser determinada a partir apenas do texto do link ou a partir do texto do link juntamente com o respectivo contexto do link determinado de forma programática, exceto quando a finalidade do link for ambígua para os usuários em geral.

#### Finalidade - Finalidade do link (Em contexto) (2.4.4)      {#purpose-link-purpose-in-context}

Para todos os usuários, independentemente da incapacidade cognitiva, indicar claramente a direção de um link por meio de um texto de link adequado é fundamental. Isso ajuda os usuários a decidir se querem ou não seguir um link. Para usuários deficientes visuais, um texto de link significativo é extremamente útil quando há vários links em uma página (principalmente se a página incluir excesso de texto), já que textos de link significativos fornecem uma indicação mais clara da funcionalidade da página de destino. Os usuários de algumas tecnologias de assistência, que podem gerar uma lista de todos os links em uma única página, poderão entender mais facilmente o texto do link fora do contexto se o texto do link for exclusivo e informativo. No entanto, indivíduos com deficiências cognitivas poderão se confundir se um link não fornecer informações suficientes para descrever com precisão onde o link os levará.

#### Como cumprir - Finalidade do link (Em contexto) (2.4.4)      {#how-to-meet-link-purpose-in-context}

Acima de tudo, verifique se a finalidade de um link está claramente descrita no texto.

* Exemplo incorreto:
   * Texto: para obter mais informações sobre nossas aulas noturnas no segundo trimestre de 2010, clique aqui .
   * Motivo: não indica clara e inequivocamente o seu destino.
* Exemplo correto:
   * Texto: aulas à noite para o segundo trimestre de 2010 - mais informações.
   * Motivo: ao ajustar levemente o texto e a posição do elemento de link, o texto pode ser melhorado:

Os links devem ser redigidos de forma consistente ao longo das páginas, principalmente em barras de navegação. Por exemplo, se um link para uma página específica for chamado de **Publicações** em uma página, use esse termo nas outras páginas para garantir a consistência.

No momento da escrita, há algumas questões relacionadas ao uso de atributos de título para garantir que links semelhantes apresentados em uma página forneçam informações exclusivas sobre o destino (por exemplo, &quot;leia mais&quot; se referirá frequentemente a uma variedade de destinos diferentes):

* O texto contido no atributo de título geralmente está disponível apenas para usuários do mouse como um pop-up de dica de ferramenta e não pode ser acessado de forma consistente usando o teclado ou por usuários móveis.
* Os leitores de tela podem ler atributos de título, mas essa funcionalidade pode não estar ativada por padrão; assim, os usuários podem não estar cientes de que existe um atributo de título.
* É difícil alterar a aparência do texto do título, o que significa que algumas pessoas podem ter dificuldade para lê-lo, ou simplesmente não conseguirem ler.

Embora o atributo de título possa ser usado para fornecer contexto adicional a um link, esteja ciente de suas limitações e não o utilize como uma alternativa ao texto de link apropriado.

Sempre que um link for constituído por uma imagem, certifique-se de que o texto alternativo para a imagem descreve o destino do link. Por exemplo, se uma imagem de uma estante de livros for definida como um link para as publicações de uma pessoa, o texto alternativo deverá informar **Publicações de John Smith** e não **Estante de livros**.

Alternativamente, se a âncora do link contém texto que descreve a finalidade do link, além do elemento de imagem (e, portanto, o texto é exibido ao lado da imagem), use um atributo alternativo vazio para a imagem:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>O snippet acima é uma ilustração; recomenda-se usar o componente **Imagem**.

Embora seja aconselhável fornecer um texto de link que identifique a finalidade do link sem a necessidade de contexto adicional, reconhece-se que isto nem sempre é possível. Link contextuais gratuitos podem ser usados nos casos a seguir, exemplos de HTML que podem ser encontrados em [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Sempre que o texto do link fizer parte de uma lista de links estritamente relacionados e quando um item de lista que delimita o link fornecer contexto suficiente.
* Sempre que a finalidade de um link puder ser claramente identificada no texto do parágrafo *anterior* (não o seguinte).
* Quando o link estiver contido em uma tabela de dados e, portanto, a finalidade puder ser claramente identificada nos cabeçalhos associados.
* Sempre que uma lista de links estiver contida em um conjunto de cabeçalhos e o próprio cabeçalho fornecer o contexto apropriado.
* Sempre que uma lista de links estiver contida em um link aninhado e o item de lista principal acima do link aninhado fornecer o contexto apropriado.

Em alguns casos, quando existirem vários links em uma página (cada um dos quais fornecendo a direção de um link em detalhes complexos, mas necessários), pode ser apropriado fornecer uma versão alternativa da página da Web que mostre exatamente o mesmo conteúdo, mas sem um texto de link tão detalhado.

Alternativamente, scripts podem ser usados &#x200B;&#x200B;de modo que uma quantidade mínima de texto seja fornecida no próprio link e, ao ativar um controle apropriado posicionado na parte superior da página, o texto do link seja *expandido* para fornecer mais detalhes. Uma abordagem semelhante é a utilização de CSS para *ocultar* o link completo para usuários deficientes visuais, mas ainda exibi-lo na íntegra para os usuários de leitores de tela. Isso está fora do âmbito deste documento, mas mais informações sobre a forma como conseguir isso podem ser encontradas na seção [Mais Informações - finalidade do Link (Em Contexto) (2.4.4)](#more-information-link-purpose-in-context).

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

Onde o critério de sucesso indicar &quot;modo de operação&quot;, deve ter em conta plataformas que nem sempre apresentam um indicador de foco. Na maioria dos casos, há apenas um modo de operação, então este critério de sucesso se aplica.

#### Como cumprir - Foco visível (2.4.7) {#how-to-meet-focus-visible}

Siga as orientações em [Como cumprir o Critério de sucesso 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Mais informações - Foco visível (2.4.7) {#more-information-focus-visible}

* [Noções sobre o Critério de sucesso 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Como cumprir o Critério de sucesso 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Princípio 3: compreensível      {#principle-understandable}

[Princípio 3: compreensível - A informação e a operação da interface do usuário devem ser compreensíveis.](https://www.w3.org/TR/WCAG/#understandable)

### Torne o conteúdo do texto legível e compreensível (3.1)      {#make-text-content-readable-and-understandable}

[Diretriz 3.1 Legível: tornar o conteúdo do texto legível e compreensível.](https://www.w3.org/TR/WCAG/#readable)

### Idioma da página (3.1.1)      {#language-of-page}

* Critério de Sucesso 3.1.1
* Nível A
* Idioma da página: o idioma humano predefinido de cada página da Web pode ser determinado de forma programática.

#### Finalidade - Idioma da página (3.1.1)      {#purpose-language-of-page}

A finalidade deste critério de sucesso é garantir que o texto e outro conteúdo linguístico sejam apresentados corretamente. Para leitores de tela, isso garante que o conteúdo seja pronunciado corretamente. Para navegadores visuais, aumenta a probabilidade de apresentar determinados conjuntos de caracteres definidos corretamente.

#### Como cumprir - Idioma da página (3.1.1)      {#how-to-meet-language-of-page}

Para cumprir este critério de sucesso, o idioma padrão de uma página da Web pode ser identificado usando o atributo `lang`dentro do elemento`<html>` no topo da página. Por exemplo:

* Se uma página for escrita em inglês, o elemento `<html>` deverá informar:
   `<html lang = “en”>`

* Para processar uma página em espanhol, deve ser adotado o seguinte padrão:
   `<html lang = “es”>`

No AEM, o idioma padrão da sua página é definido ao criar página, mas também pode ser alterado ao editar as [Propriedades da Página](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>O AEM fornece mais ajuste para variações de um idioma raiz; por exemplo, inglês americano - en-us, inglês britânico - en-gb, e inglês canadense - en-ca. Esse nível de detalhes é geralmente supérfluo para a tecnologia de assistência, embora possa ser usado para variações regionais no conteúdo da página.

#### Mais Informações - Idioma da Página (3.1.1) {#more-information-language-of-page}

* [Noções sobre o Critério de sucesso 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Como cumprir o Critério de sucesso 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Os códigos são baseados em ISO 639-1. Uma lista mais extensa de códigos para cada idioma pode ser encontrada no [site W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de Partes (3.1.2)            {#language-of-parts}

* Critério de Sucesso 3.1.2
* Nível AA
* Idioma de Partes: o idioma humano de cada passagem ou frase do conteúdo pode ser determinado de forma programática, exceto para os nomes próprios, termos técnicos, palavras de idioma indeterminado e palavras ou frases que se tornaram parte do vernáculo do texto imediatamente circundante.

#### Finalidade - Idioma de Partes (3.1.2)      {#purpose-language-of-parts}

A finalidade deste critério de sucesso é semelhante ao critério de sucesso de [Idioma da Página ](#language-of-page), exceto que se aplica a páginas da Web com conteúdo em múltiplos idiomas em uma única página (por exemplo, devido a citações ou palavras incomuns).

As páginas que aplicam este critério de sucesso:

* Permitem que o software de tradução em braille insira caracteres acentuados.
* Leitores de tela para pronunciar as palavras que têm caracteres especiais ou que não estão no idioma padrão identificado no nível da página.
* Permitem que as ferramentas de tradução, como o Google Translate, traduzam corretamente o conteúdo de um idioma para outro.

#### Como Cumprir - Idioma de Partes (3.1.2)      {#how-to-meet-language-of-parts}

O atributo `lang` pode ser utilizado para identificar alterações no idioma do conteúdo. Por exemplo, uma citação em alemão (ISO 639-1, código “de”) pode ser apresentada da seguinte maneira:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Blocos de citação não são suportados em uma instância predefinida. Um componente personalizado pode ser desenvolvido para suportar o recurso.

Da mesma forma, o navegador poderá processar uma palavra incomum ou frase corretamente se o elemento `span` for usado da seguinte maneira:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Não é necessário seguir este critério de sucesso ao incluir nomes ou cidades em diferentes idiomas, ou ao usar palavras de empréstimo ou frases que se tornaram comuns no idioma padrão (como *schadenfreude* em inglês).

Para adicionar o elemento span, com um idioma apropriado, você pode editar manualmente a sua marcação HTML no modo de edição de fonte da RTE para ser exibido como acima. Como alternativa, o atributo `lang`[ pode ser incluído na RTE pelo administrador do sistema (consulte Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

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

O foco pode ser movido para um controle por meio do teclado (por exemplo, tabulação de um controle) ou do mouse (por exemplo, clique em um campo de texto). Mover o mouse sobre um controle não move o foco, a menos que o script implemente esse comportamento. Observe que para alguns tipos de controles, clicar em um controle também pode ativá-lo (por exemplo, botão), que pode, por sua vez, iniciar uma alteração no contexto.

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

O propósito deste Critério de sucesso é garantir que a inserção de dados ou a seleção de um controle de formulário tenha efeitos previsíveis. Alterar a configuração de qualquer componente da interface do usuário altera algum aspecto no controle que persistirá quando o usuário não estiver mais interagindo com ele. Portanto, marcar uma caixa de seleção, inserir texto em um campo de texto ou alterar a opção selecionada em um controle de lista altera sua configuração, mas ativar um link ou um botão não altera. As alterações no contexto podem confundir os usuários que não percebem facilmente a mudança ou que são facilmente distraídos por mudanças. As alterações de contexto são apropriadas apenas quando estiver claro que tal alteração ocorrerá em resposta à ação do usuário.

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

O propósito deste Critério de sucesso é incentivar o uso de apresentação e layout consistentes para usuários que interagem com conteúdo repetido em um conjunto de páginas da Web e precisam localizar informações ou funcionalidades específicas mais de uma vez. Os indivíduos com pouca visão que usam ampliação de tela para exibir uma pequena parte da tela por vez geralmente usam dicas visuais e limites de página para localizar rapidamente o conteúdo repetido. Apresentar conteúdo repetido na mesma ordem também é importante para os usuários visuais que usam memória espacial ou dicas visuais no design para localizar conteúdo repetido.

É importante observar que utilizar a frase &quot;mesma ordem&quot; nesta seção não significa que os menus de subnavegação não possam ser usados ou que blocos de navegação secundária ou estrutura de página não possam ser usados. Em vez disso, este Critério de sucesso destina-se a ajudar os usuários que interagem com conteúdo repetido em várias páginas da Web a prever a localização do conteúdo que estão procurando e localizá-lo mais rapidamente quando o encontrarem novamente.

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

O propósito deste Critério de sucesso é garantir a identificação consistente de componentes funcionais que aparecem repetidamente em um conjunto de páginas da Web. Uma estratégia que as pessoas que usam leitores de tela usam ao operar um site é contar com a familiaridade com funções que podem aparecer em diferentes páginas da Web. Se funções idênticas tiverem rótulos diferentes (ou, de forma geral, um nome acessível diferente) em diferentes páginas da Web, o site será mais difícil de usar. Pode também ser confuso e aumentar a carga cognitiva de pessoas com limitações cognitivas. Sendo assim, uma rotulagem coerente ajudará.

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

O propósito deste Critério de sucesso é garantir que os usuários estejam cientes de que ocorreu um erro e possam determinar o que está errado. A mensagem de erro deve ser o mais específica possível. No caso de um envio de formulário malsucedido, a reexibição do formulário e a indicação dos campos com erro são insuficientes para que alguns usuários percebam que ocorreu um erro. Os usuários do leitor de tela, por exemplo, não saberão que houve um erro até encontrarem um dos indicadores. Eles podem abandonar o formulário completamente antes de encontrar o indicador de erro, achando que a página simplesmente não está funcionando. Per the definition in WCAG, an [input error](https://www.w3.org/TR/WCAG/#dfn-input-error) is information provided by the user that is not accepted. Isso inclui:

informações exigidas pela página da Web, mas omitidas pelo usuário ou informações fornecidas pelo usuário, mas que não estejam no formato de dados necessário ou valores permitidos.
Por exemplo:

* o usuário não digita a abreviação adequada em estado, província, região etc. campo;
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

### Etiquetas ou Instruções (3.3.2)      {#labels-or-instructions}

* Critério de Sucesso 3.3.2
* Nível A
* Etiquetas ou Instruções: as etiquetas ou instruções são fornecidas quando o conteúdo exigir a entrada do usuário.

#### Finalidade - Etiquetas ou Instruções (3.3.2)      {#purpose-labels-or-instructions}

Fornecer instruções para ajudar as pessoas a preencher formulários é uma parte fundamental das boas práticas de usabilidade da interface. Fazer isso é particularmente útil para pessoas com deficiências visuais ou cognitivas que de outra forma poderiam ter dificuldade para entender o layout de um formulário e o tipo de dados a ser fornecido em um campo de formulário específico.

##### Forms

In the AEM WKND demo project a default label is added when you add a form component, such as a **Text Field**, to the page. Este título padrão é dependente do tipo de componente. Você pode adicionar seu próprio título na guia **Título e Texto** da janela de edição desse campo. É importante garantir que as etiquetas ajudem os usuários a compreender os dados associados a cada componente do formulário.

Este campo de **Título** deve ser usado para elementos de campo, pois fornece uma etiqueta que está disponível para tecnologia assistiva. Apenas escrever uma etiqueta no texto ao lado do campo não é suficiente.

Para alguns componentes de formulário, também é possível ocultar as etiquetas visualmente usando a opção **Ocultar Título**. Marcadores ocultos ainda estão disponíveis para a tecnologia assistiva, mas não são exibidos na tela. Embora esta possa ser uma boa abordagem em algumas situações, geralmente é melhor incluir uma etiqueta visual sempre que possível, pois alguns usuários podem estar olhando para uma pequena seção da tela (um campo por vez) e precisam de etiquetas para identificar o campo corretamente.

###### Botões de imagem {#image-buttons}

Where image buttons are used (for example, the **Image Button** component of the WKND project) the **Title** field in the **Title and Text** tab of the edit dialog actually provides the alt text for the image, rather than the label. Assim, no exemplo abaixo, a imagem com o texto `Submit`tem o texto alternativo de `Submit`, adicionado usando o campo **Título** na janela de edição.

###### Grupos de campos de formulário {#groups-of-form-fields}

In the WKND project, where there is a group of related controls, such as **Radio Group**, a title may be needed for the group, as well as individual controls. Ao adicionar um conjunto de botões de opção no AEM, o campo **Título** fornece esse título de grupo, enquanto títulos individuais são especificados conforme os botões de opção (**Itens**) são criados.

Contudo, não existe uma associação programática entre o título do grupo e os próprios botões de opção. Editores de modelo precisam envolver o título nas tags `fieldset` e `legend` necessárias para criar esta associação e isso só pode ser feito através da edição do código fonte da página. Alternativamente, um administrador do sistema pode adicionar suporte a esses elementos para que eles apareçam na janela **Propriedades do Campo**[ (Consulte Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

###### Considerações adicionais para formulários {#additional-considerations-for-forms}

Se os dados devem ser inseridos em um formato específico, deixe isso claro no texto da etiqueta. Por exemplo, se uma data deve ser inscrita no formato `DD-MM-YYYY`, indique isso especificamente como parte da etiqueta. Isto significa que quando os usuários de leitores de tela encontrarem o campo, a etiqueta será anunciada automaticamente, juntamente com as informações adicionais sobre o formato.

Se a entrada de um campo de formulário for obrigatória, deixe isso claro usando a palavra &quot;obrigatório&quot; como parte do rótulo. O AEM adiciona um asterisco quando um campo é obrigatório, mas seria ideal incluir a palavra `required` na própria etiqueta (no campo **Título** na janela de edição).

O posicionamento das etiquetas também é importante, pois ajuda a localizar os campos apropriados. Isto é de especial importância quando o usuário se depara com um formulário complexo. Siga a convenção abaixo:

* As caixas de seleção ou botões de opção:
As etiquetas são posicionadas imediatamente à direita do campo.
* Todos os outros componentes do formulário (por exemplo, caixas de texto, caixas de combinação):
As etiquetas são posicionadas imediatamente acima ou à esquerda do campo.

Em formulários simples, com funcionalidade muito limitada, a identificação adequada de um botão `Submit` pode servir como etiqueta para o campo adjacente (por exemplo, `Search`). Isso é útil em situações em que encontrar espaço para o texto da etiqueta pode ser difícil.

#### Mais Informações - Etiquetas ou Instruções (3.3.2)      {#more-information-labels-or-instructions}

* [Noções sobre o Critério de sucesso 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Como cumprir o Critério de sucesso 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Sugestão de erro (3.3.3)  {#error-suggestion}

* Critério de Sucesso 3.3.3
* Nível AA
* Teclado: se um erro de entrada for detectado automaticamente e as sugestões para correção forem conhecidas, as sugestões serão fornecidas ao usuário, a menos que isso comprometa a segurança ou o propósito do conteúdo.

#### Propósito - Sugestão de erro (3.3.3) {#purpose-error-suggestion}

O propósito deste Critério de sucesso é garantir que os usuários recebam sugestões adequadas para a correção de um erro de entrada, se possível. The WCAG definition of [input error](https://www.w3.org/TR/WCAG/#dfn-input-error) says that it is &quot;information provided by the user that is not accepted&quot; by the system. Alguns exemplos de informações que não são aceitas incluem informações obrigatórias, mas omitidas pelo usuário, e informações fornecidas pelo usuário, mas que não estão no formato de dados necessário ou valores permitidos.

O Critério de sucesso 3.3.1 prevê a notificação de erros. Mas as pessoas com limitações cognitivas podem ter dificuldade para entender como corrigir os erros. Pessoas com deficiências visuais podem não ser capazes de descobrir exatamente como corrigir o erro. No caso de um envio de formulário malsucedido, os usuários podem abandonar o formulário por não ter certeza de como corrigir o erro, mesmo sabendo que ele ocorreu.

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

O propósito deste Critério de sucesso é ajudar os usuários portadores de deficiências a evitarem consequências graves como resultado de um erro ao executar uma ação que não pode ser revertida. Por exemplo, a compra de passagens não reembolsáveis ou a apresentação de uma ordem de compra de ações numa conta de corretagem são transações financeiras com graves consequências. Se um usuário tiver cometido um erro na data da passagem aérea, poderá receber um bilhete no dia errado que não poderá ser trocado. Se tiver cometido um erro no número de ações a serem compradas, poderia acabar comprando mais ações do que o esperado. Ambos os tipos de erros envolvem transações que ocorrem imediatamente e não podem ser alteradas depois, e podem ser muito caras. Da mesma forma, pode ser um erro irrecuperável se os usuários modificarem ou excluírem involuntariamente os dados armazenados em um banco de dados que precisarão acessar posteriormente, como todo o perfil de viagem em um site de serviços de viagens. No que se refere à modificação ou exclusão de dados &#39;controláveis pelo usuário&#39;, a intenção é evitar a perda em massa de dados, como a exclusão de um arquivo ou registro. Não é a intenção exigir uma confirmação de cada comando save ou a simples criação ou edição de documentos, registros ou outros dados.

Os usuários portadores de deficiências podem ter mais probabilidade de cometer erros. As pessoas com deficiências de leitura podem transpor números e letras, e aquelas com deficiências motoras podem apertar as teclas por engano. Fornecer a capacidade de reverter ações permite que os usuários corrijam um erro que pode resultar em consequências graves. Fornecer a capacidade de revisar e corrigir informações dá ao usuário a oportunidade de detectar um erro antes de tomar uma ação que tenha consequências graves.

Os dados controláveis pelo usuário são dados visualizáveis pelo usuário que ele pode alterar e/ou excluir por meio de uma ação intencional. Os exemplos de usuários que controlam esses dados seriam a atualização do número de telefone e do endereço da conta do usuário ou a exclusão de um registro de faturas anteriores de um site. Eles não se referem a coisas como registros da Internet e dados de monitoramento de mecanismos de busca com os quais o usuário não pode visualizar ou interagir diretamente.

#### Como cumprir - Prevenção de erros (legal, financeiro, dados) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Siga as orientações em [Como cumprir o Critério de sucesso 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Mais informações - Prevenção de erros (legal, financeiro, dados) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Noções sobre o Critério de sucesso 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Como cumprir o Critério de sucesso 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Princípio 4: Robusto {#principle-robust}

[Princípio 4: Robusto - o conteúdo deve ser robusto o suficiente para que possa ser interpretado por uma grande variedade de agentes do usuário, incluindo tecnologias assistivas.](https://www.w3.org/TR/WCAG/#robust)

### Compatível (4.1) {#compatible}

[Compatível com a diretriz 4.1: aumente a compatibilidade com os agentes do usuário atuais e futuros, incluindo as tecnologias assistivas.](https://www.w3.org/TR/WCAG/#compatible)

Aumente a compatibilidade com os agentes do usuário atuais e futuros, incluindo as tecnologias assistivas.

### Análise (4.1.1)  {#parsing}

* Critério de Sucesso 4.1.1
* Nível A
* Análise: no conteúdo implementado que usa idiomas de marcação, os elementos têm tags de início e fim completas, os elementos são aninhados de acordo com as especificações, os elementos não contêm atributos duplicados e as IDs são exclusivas, exceto quando as especificações permitem esses recursos.

#### Propósito - Análise (4.1.1) {#purpose-parsing}

O propósito deste Critério de sucesso é garantir que os agentes do usuário, incluindo as tecnologias assistivas, possam interpretar e analisar o conteúdo com precisão. Se o conteúdo não puder ser analisado em uma estrutura de dados, agentes do usuário diferentes poderão apresentá-lo de forma diferente ou não poderão analisá-lo completamente. Alguns agentes do usuário usam &quot;técnicas de reparo&quot; para renderizar conteúdo mal codificado.

Como as técnicas de reparo variam entre os agentes do usuário, os autores não podem assumir que o conteúdo será analisado com precisão em uma estrutura de dados ou que será renderizado corretamente por agentes do usuário especializados, incluindo tecnologias assistivas, a menos que o conteúdo seja criado de acordo com as regras definidas na gramática formal dessa tecnologia. Em idiomas de marcação, erros na sintaxe do elemento e no não fornecimento de tags de início/fim aninhadas corretamente levam a erros que impedem os agentes do usuário de analisar o conteúdo de forma confiável. Portanto, o Critério de sucesso exige que o conteúdo possa ser analisado usando apenas as regras da gramática formal.

#### Como cumprir - Análise (4.1.1) {#how-to-meet-parsing}

Siga as orientações em [Como cumprir o Critério de sucesso 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Mais informações - Análise (4.1.1) {#more-information-parsing}

* [Noções sobre o Critério de sucesso 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Como cumprir o Critério de sucesso 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nome, função, valor (4.1.2)  {#name-role-value}

* Critério de Sucesso 4.1.2
* Nível A
* Nome, Função, Valor: para todos os componentes da interface do usuário (incluindo, mas não limitados a: elementos de formulário, links e componentes gerados por scripts), o nome e a função podem ser determinados de forma programática; estados, propriedades e valores que podem ser definidos pelo usuário podem ser definidos de forma programática; e a notificação de alterações nesses itens está disponível aos agentes do usuário, incluindo tecnologias assistivas.

#### Propósito - Nome, Função, Valor (4.1.2) {#purpose-ame-role-value}

O propósito deste Critério de sucesso é garantir que as Tecnologias assistivas (AT) possam coletar informações sobre, ativar ou definir e manter-se atualizadas sobre o status dos controles da interface do usuário no conteúdo.

Quando controles padrão de tecnologias assistivas são usados, esse processo é simples. Se os elementos da interface do usuário forem usados de acordo com as especificações, as condições desta provisão serão atendidas. (Veja os exemplos do Critério de sucesso 4.1.2 abaixo)

No entanto, se os controles personalizados forem criados ou se os elementos de interface forem programados (em código ou script) para terem uma função e/ou função diferente da usual, então é necessário tomar medidas adicionais para garantir que os controles forneçam informações importantes para as tecnologias assistivas e permitam que eles sejam controlados por tecnologias assistivas.

Um estado particularmente importante de um controle da interface do usuário é se ele tem ou não foco. O estado de foco de um controle pode ser determinado de forma programática e as notificações sobre mudança de foco são enviadas aos agentes do usuário e à tecnologia de assistência. Outros exemplos de estado de controle da interface do usuário são se uma caixa de seleção ou um botão de opção foi selecionado ou se um nó de árvore ou de lista que pode ser recolhido foi expandido ou recolhido.

#### Como cumprir - Nome, Função, Valor (4.1.2) {#how-to-meet-ame-role-value}

Siga as orientações em [Como cumprir o Critério de sucesso 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Mais informações - Nome, função, valor (4.1.2 {#more-information-ame-role-value}

* [Noções sobre o Critério de sucesso 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Como cumprir o Critério de sucesso 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
