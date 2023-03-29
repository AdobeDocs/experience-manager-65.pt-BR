---
title: Criação de conteúdo acessível (Conformidade com a WCAG 2.0)
seo-title: Creating Accessible Content (WCAG 2.0 Conformance)
description: A WCAG 2.0 consiste em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável para pessoas com necessidades especiais.
seo-description: WCAG 2.0 consists of a set of technology independent guidelines and success criteria to help make web content accessible to, and usable by, persons with disabilities.
page-status-flag: de-activated
uuid: c2c0cac0-2a9f-478d-8261-e8cc894aae34
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 378bc33d-ab6c-4651-9688-102c961561fc
exl-id: 01c69aa9-2623-42dc-9e2d-62bc5e01cf0e
source-git-commit: ce6d24e53a27b64a5d0a9db2e4b6672bd77cf9ec
workflow-type: tm+mt
source-wordcount: '9153'
ht-degree: 32%

---

# Criação de conteúdo acessível (Conformidade com a WCAG 2.0)  {#creating-accessible-content-wcag-conformance}

>[!CAUTION]
>
>Como a interface clássica foi descontinuada no AEM 6.4, o conteúdo desta página não foi atualizado para a WCAG 2.1.
>
>Consulte as seguintes páginas para obter detalhes relacionados ao AEM e à WCAG 2.1:
>
>* [AEM e as diretrizes de acessibilidade na Web](/help/managing/web-accessibility.md)
>* [Um guia rápido para a WCAG 2.1](/help/managing/qg-wcag.md)
>* [Criação de conteúdo acessível (Conformidade com o WCAG 2.1)](/help/sites-authoring/creating-accessible-content.md)


A WCAG 2.0 consiste em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável para pessoas com necessidades especiais.

>[!NOTE]
>
>Consulte também:
>
>* [Guia rápido para a WCAG 2.0](/help/managing/qg-wcag.md)
>* [Configurar o Editor de Rich Text para a produção de conteúdo acessível](/help/sites-administering/rte-accessible-content.md)
>


Essas diretrizes são classificadas de acordo com três níveis de conformidade: Nível A (o mais baixo), Nível AA e Nível AAA (o mais alto). Resumidamente, os níveis são definidos da seguinte maneira:

* **Nível A**: o site atinge um nível mínimo básico de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A são cumpridos.
* **Nível AA:** O nível ideal de acessibilidade que você deve almejar, no qual seu site atinge um nível aprimorado de acessibilidade, para que seja acessível à maioria das pessoas na maioria das situações usando a maioria das tecnologias. Para atingir esse nível, todos os Critérios de sucesso do Nível A e Nível AA são cumpridos.
* **Nível AAA:** O site atinge um nível muito elevado de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A, Nível AA e Nível AAA são cumpridos.

Ao criar o seu site, é necessário determinar o nível global com o qual você gostaria que ele estivesse em conformidade.

A seção a seguir apresenta as [Diretrizes da WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) com os critérios de sucesso relacionados aos [níveis de conformidade](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) A e AA.

>[!NOTE]
>
>Como não é possível cumprir todos os Critérios de sucesso de Nível AAA para certos tipos de conteúdo, não é recomendável que esse nível de conformidade seja exigido como uma política geral.

>[!NOTE]
>
>Este documento usa o seguinte:
>
>* os nomes curtos para as [Diretrizes da WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines).
>* a numeração usada nas [Diretrizes da WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) para auxiliar na referência cruzada com o site da WCAG.
>


## Princípio 1: perceptível    {#principle-perceivable}

[Princípio 1: perceptível - As informações e os componentes da interface do usuário têm de ser apresentados aos usuários de formas perceptíveis.](https://www.w3.org/TR/WCAG20/#perceivable)

### Alternativas em texto (1.1)       {#text-alternatives}

[Diretriz 1.1 Alternativas em texto: Fornece alternativas em texto para qualquer conteúdo não textual, para que seja possível alterá-lo para outras formas mais adequadas à necessidade do indivíduo, como impressão em caracteres ampliados, braille, fala, símbolos ou linguagem mais simples.](https://www.w3.org/TR/WCAG20/#text-equiv)

### Conteúdo não textual (1.1.1) {#non-text-content}

* Critério de Sucesso 1.1.1
* Nível A
* Conteúdo não textual: todo o conteúdo não textual que é apresentado ao usuário tem uma alternativa em texto que serve um propósito equivalente, exceto para as situações indicadas abaixo.

#### Finalidade - Conteúdo não textual (1.1.1) {#purpose-non-text-content}

As informações em uma página da Web podem ser fornecidas em vários formatos não textuais diferentes, como imagens, vídeos, animações, gráficos e gráficos. Os indivíduos cegos ou com deficiências visuais graves não conseguem visualizar o conteúdo não textual, mas podem acessar o conteúdo do texto fazendo com que ele seja lido por um leitor de tela ou apresentado na forma tátil por um dispositivo de exibição em Braille. Assim, ao fornecer alternativas em texto para o conteúdo em formato gráfico, as pessoas que não conseguem ver que o conteúdo gráfico pode acessar uma versão equivalente das informações fornecidas pelo conteúdo.

Um benefício adicional útil é que as alternativas em texto permitem que o conteúdo não textual seja indexado pela tecnologia do mecanismo de pesquisa.

#### Como cumprir - Conteúdo não textual (1.1.1) {#how-to-meet-non-text-content}

Para gráficos estáticos, o requisito básico é o de proporcionar uma alternativa em texto equivalente para o gráfico. Esse método é feito na variável **Texto alternativo** campo :

>[!NOTE]
>
>Alguns componentes prontos para uso, como o **Carrossel** e a **Apresentação de slides**, não fornecem um meio de adicionar descrições de texto alternativas a imagens. Ao implementar versões desses componentes para a instância de AEM, a equipe de desenvolvimento deve configurá-los para dar suporte à variável `alt` atributo. Isso garante que os autores possam adicioná-lo ao conteúdo (consulte [Adicionar suporte para elementos e atributos de HTML adicionais](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

O **Texto alternativo** está disponível na variável **Avançado** guia de propriedades da imagem do **Imagem** caixa de diálogo do componente:

![Caixa de diálogo Editar do componente de Imagem na interface clássica; mostra o campo Texto alternativo .](assets/chlimage_1-17a.png)

AEM adiciona uma **Texto alternativo** para suas imagens por padrão. Para a interface clássica, há dois cenários diferentes para a forma como o atributo padrão é criado, embora o valor padrão possa não ser suficiente como uma alternativa e provavelmente deve ser editado na variável **Avançado** guia de propriedades da imagem:

* Arquivo:

Uma imagem é carregada do disco rígido do usuário. Se você adicionar um componente de imagem a uma página e, em seguida, escolher uma imagem do seu disco rígido ou de outra fonte, o valor padrão de **Texto alternativo** é `file`. Esse valor deve ser alterado no **Avançado** guia de propriedades da imagem. Novamente, esse valor não é exibido na variável **Texto alternativo** , mas quando o valor é alterado, o novo valor é exibido no campo .

* Ativo:

Uma imagem é adicionada do repositório de ativos digitais. Se você arrastar uma imagem do repositório de ativos digitais para uma página da Web, então a variável **Título** e **Texto alternativo** Os valores dessa imagem são obtidos dos metadados para essa imagem.

>[!NOTE]
>
>Em ambos os cenários acima, o padrão **Texto alternativo** não é visível na variável **Propriedades avançadas de imagem** guia . Para alterar o valor padrão, basta inserir um novo valor na variável **Texto alternativo** campo.

>[!NOTE]
>
>Se a imagem for meramente decorativa (consulte [Criar boas alternativas de texto](#creating-good-text-alternatives)), você pode inserir um espaço no **Texto alternativo** usando a barra de espaço. Isso cria um vazio `alt` , que solicita que um leitor de tela ignore a imagem.

#### Criar boas alternativas de texto {#creating-good-text-alternatives}

Existem várias formas de conteúdo não textual, portanto, o valor da alternativa em texto depende da função que o gráfico desempenha na página da Web. Algumas regras gerais incluem:

* As alternativas em texto devem ser sucintas, mas devem capturar claramente as informações essenciais fornecidas pelo conteúdo não textual.
* Descrições excessivamente longas (mais de 100 caracteres) devem ser evitadas. Se um texto alternativo exigir mais detalhes:

   * forneça uma breve descrição no texto alternativo
   * e ter uma descrição mais longa no texto em outro lugar na mesma página ou em uma página separada. Vincule para essa descrição separada, tornando a imagem um link ou colocando um link de texto ao lado da imagem.

* O texto alternativo não deve replicar o conteúdo fornecido no formulário de texto próximo à mesma página. Lembre-se de que muitas imagens são ilustrações de pontos já abordados no texto de uma página; portanto, talvez já exista uma alternativa detalhada em texto.
* Se o conteúdo não textual for um link para outra página ou documento e não houver nenhum outro texto que faça parte do mesmo link, o texto alternativo da imagem deverá indicar o destino do link. Ela não deve descrever a imagem.
* Se o conteúdo não textual estiver em um elemento de botão e não houver texto que faça parte do mesmo botão, o texto alternativo da imagem deverá indicar a funcionalidade do botão, não descrever a imagem.
* É aceitável que uma imagem receba um texto vazio (nulo), alternativo, mas somente se a imagem não tiver um texto alternativo. Por exemplo, é um gráfico meramente decorativo. Ou, se o texto equivalente já existir no texto da página.

O [Rascunho W3C: Técnicas do HTML5 para fornecer alternativas em texto úteis](https://html.spec.whatwg.org/multipage/images.html#alt) O tem mais detalhes e exemplos da disposição adequada do texto alternativo para imagens de diferentes tipos.

Tipos específicos de conteúdo não textual que necessitam de alternativas em texto podem incluir:

* Fotos ilustrativas:

Estas são imagens de pessoas, objetos ou lugares. Reflita sobre a função da foto na página; é provável que um equivalente em texto adequado seja *Foto de [objeto]*, mas pode depender do contexto.

* Ícones:

Pequenos pictogramas (gráficos) que transmitem informações específicas. Eles devem ser usados de forma consistente em uma página e um site. Todas as instâncias do ícone em uma página ou um site devem ter a mesma alternativa em texto curta e sucinta, a menos que isso resulte em duplicação desnecessária do texto adjacente.

* Gráficos e gráficos:

Normalmente, representam dados numéricos. Dessa forma, uma opção para fornecer uma alternativa em texto pode ser incluir um breve resumo das principais tendências mostradas no gráfico ou gráfico. Se necessário, forneça também uma descrição mais detalhada no texto usando a variável **Descrição** no campo **Avançado** guia de propriedades da imagem. Além disso, você pode fornecer os dados de origem em forma de tabela em outro lugar na página ou no site.

![Exemplo de gráfico. Abaixo está a melhor abordagem para fornecer uma alternativa.](assets/chlimage_1-2a.jpeg)

Para fornecer uma alternativa para esse gráfico de exemplo, adicione um resumo `alt` texto para a própria imagem e, em seguida, siga a imagem com uma alternativa em texto completa.

```xml
<p><img src="figure1.gif" alt="Figure 1" ></p>
<p> Figure 1. Distribution of Articles by Journal Category.
Pie chart: Language=68%, Education=14% and Science=18%.</p>
```

>[!NOTE]
>
>O trecho acima é usado apenas para ilustrar a ordem. Use o **Imagem** , em vez de `img src` referência usada acima.

No AEM, você pode usar uma combinação do **Texto alternativo** e **Descrição** campos na caixa de diálogo de configuração da imagem - como em [Como cumprir - Conteúdo não textual (1.1.1)](#how-to-meet-non-text-content).

* Mapas, diagramas, fluxogramas:

Para gráficos que fornecem dados espaciais (por exemplo, para ser compatível com a descrição das relações entre objetos ou um processo), verifique se a mensagem principal é fornecida no formato de texto.  Para mapas, fornecer um equivalente de texto completo provavelmente não será prático, mas se o mapa for fornecido como uma maneira de ajudar as pessoas a encontrar o caminho para um determinado local, o texto alternativo da imagem do mapa poderá indicar brevemente a informação *Mapa de X* e, em seguida, fornecer instruções para acessar esse local no texto de outro lugar da página ou por meio do campo **Descrição** na guia **Avançado** do componente **Imagem**.

* CAPTCHAs:

Um CAPTCHA é um *Teste de Turing público completamente automatizado para diferenciar computadores e humanos*. É uma verificação de segurança usada em páginas da Web para distinguir seres humanos de software mal-intencionado, mas que pode causar barreiras de acessibilidade. São imagens que exigem que os usuários descrevam o que veem para passar em um teste de segurança. Não é possível fornecer uma alternativa em texto para a imagem, portanto, em vez disso, você deve considerar soluções alternativas não gráficas.

O W3C fornece várias sugestões, como a seguinte. Cada uma destas abordagens tem os seus próprios méritos e desvantagens.

    * Quebras de linha lógica
    * O uso da saída de som em vez de imagens
    * Contas de uso limitadas e filtros de spam.

* Imagens de plano de fundo:

Essas imagens são obtidas usando a Cascading Style Sheets (CSS), em vez de no HTML. Não é possível especificar um valor de texto alternativo. Portanto, as imagens de plano de fundo não devem fornecer informações textuais importantes - se o fizerem, também devem ser fornecidas no texto da página.

No entanto, é importante que um plano de fundo alternativo seja exibido quando a imagem não puder ser exibida.

>[!NOTE]
>
>Deve haver um nível adequado de contraste entre o plano de fundo e o texto de primeiro plano. Este contraste é discutido com mais pormenor em [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Mais informações - Conteúdo não contextual (1.1.1) {#more-information-non-text-content}

* [Noções sobre o Critério de sucesso 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [Como cumprir o Critério de sucesso 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#text-alternatives)
* [W3C: Técnicas do HTML5 para fornecer alternativas em texto úteis](https://html.spec.whatwg.org/multipage/images.html#alt)
* [Explicação do W3C sobre as alternativas para CAPTCHAs](https://www.w3.org/TR/turingtest/)

### Mídia com base no tempo (1.2)       {#time-based-media}

[Diretriz de mídia com base no tempo 1.2: Fornecer alternativas para a mídia com base no tempo.](https://www.w3.org/TR/WCAG20/#text-equiv)

Essas informações lidam com o conteúdo da Web que é *baseado no tempo*. Abrange o conteúdo que o usuário pode reproduzir (como vídeo, áudio e conteúdo animado) e pode ser pré-gravado ou ter transmissão ao vivo.

### Apenas áudio e apenas vídeo (pré-gravado) (1.2.1)    {#audio-only-and-video-only-pre-recorded}

* Critério de sucesso 1.2.1
* Nível A
* Apenas áudio e apenas vídeo (pré-gravado): Para mídia somente de áudio e somente de vídeo pré-gravada, as opções a seguir são verdadeiras, exceto quando o áudio ou vídeo for uma alternativa de mídia para texto e claramente identificada como tal:

   * Apenas áudio pré-gravado: É fornecida uma alternativa para a mídia com base no tempo, que apresenta informações equivalentes para o conteúdo somente de áudio pré-gravado.
   * Apenas vídeo pré-gravado: É fornecida uma alternativa para a mídia com base no tempo ou uma faixa de áudio que apresenta informações equivalentes para o conteúdo somente de vídeo pré-gravado.

#### Propósito - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1)    {#purpose-audio-only-and-video-only-pre-recorded}

Problemas de acessibilidade para vídeo e áudio podem ser enfrentados por:

* Pessoas com deficiências visuais quando não há trilha sonora ou a trilha sonora não é suficiente para informá-las do que está acontecendo no vídeo ou animação;
* Pessoas com deficiências auditivas ou surdas, que não conseguem ouvir a trilha sonora;
* Pessoas que podem ouvir a trilha sonora, mas não entendem o que está sendo falado (por exemplo, porque está em um idioma que não entendem).

O vídeo ou áudio também pode estar indisponível para pessoas que usam navegadores ou dispositivos que não oferecem suporte à reprodução de conteúdo em formatos de mídia específicos, como o Flash de Adobe.

Fornecer essas informações em um formato diferente, como texto (ou áudio para vídeo sem áudio), pode torná-lo acessível para pessoas que não conseguem acessar o conteúdo original.

#### Como cumprir - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1)    {#how-to-meet-audio-only-and-video-only-pre-recorded}

* Se o conteúdo for um áudio pré-gravado sem vídeo (como um podcast):

   * Forneça um link imediatamente antes ou depois do conteúdo para obter uma transcrição do texto do conteúdo de áudio.

   A transcrição deve ser uma HTML page com um equivalente em texto de todo o conteúdo falado e não-falado importante. Também deve indicar quem está falando, uma descrição do cenário, expressões vocais e uma descrição de qualquer outro áudio significativo.

* Se o conteúdo for uma animação ou vídeo pré-gravado sem áudio:

   * Forneça um link imediatamente antes ou depois do conteúdo para uma descrição de texto equivalente das informações fornecidas pelo vídeo
   * Ou uma descrição de áudio equivalente em um formato de áudio normalmente usado, como MP3.

>[!NOTE]
>
>Se o conteúdo de áudio ou vídeo for fornecido como uma alternativa ao conteúdo que existe em outro formato em uma página da Web, não será necessário seguir os requisitos acima. Por exemplo, se um vídeo ilustra uma lista de instruções de texto, ele não requer uma alternativa, pois as instruções de texto já atuam como uma alternativa ao vídeo.

Inserir multimídia, especificamente conteúdo de Flash, em suas páginas da Web AEM é semelhante à inserção de uma imagem. No entanto, como o conteúdo multimídia é muito maior do que uma imagem estática, há várias configurações e opções diferentes para controlar a forma como a multimídia é reproduzida.

>[!NOTE]
>
>Ao usar multimídia com um conteúdo informativo, é necessário criar também links para as alternativas. Por exemplo, para incluir uma transcrição de texto, crie uma página HTML para exibir a transcrição e, em seguida, adicione um link ao lado ou abaixo do conteúdo de áudio.

#### Mais informações - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [Como cumprir o Critério de sucesso 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#time-based-media)

### Legendas (pré-gravadas) (1.2.2)    {#captions-pre-recorded}

* Critério de sucesso 1.2.2
* Nível A
* Legendas (pré-gravadas): as legendas são disponibilizadas para todo o conteúdo de áudio pré-gravado na multimídia sincronizada, exceto quando a mídia é uma alternativa para texto e é claramente identificada como tal.

#### Propósito - Legendas (pré-gravadas) (1.2.2)    {#purpose-captions-pre-recorded}

Os indivíduos surdos ou com deficiência auditiva não conseguem ou têm grande dificuldade ao acessar o conteúdo de áudio. As legendas são equivalentes em texto para áudio falado e não falado, exibidas na tela no momento adequado durante o vídeo. Eles permitem que os indivíduos que não conseguem ouvir o áudio entendam o que está acontecendo.

>[!NOTE]
>
>As legendas não são necessárias onde o texto adequado ou equivalentes não textuais (que fornecem informações diretamente equivalentes) estão disponíveis na mesma página que o vídeo ou a animação.

#### Como cumprir - Legendas (pré-gravadas) (1.2.2)    {#how-to-meet-captions-pre-recorded}

As legendas podem ser:

* Abertas: sempre visíveis quando o vídeo é reproduzido
* Ocultas: as legendas podem ser ativadas ou desativadas pelo usuário

Use as legendas ocultas sempre que possível. Ele oferece aos usuários a opção de exibir legendas.

Para legendas ocultas, crie e forneça um arquivo de legenda sincronizada em um formato apropriado, como [SMIL](https://www.w3.org/AudioVideo/), juntamente com o arquivo de vídeo.

Consulte os tutoriais em [Mais informações - Legendas (pré-gravadas) (1.2.2)](#more-information-captions-pre-recorded). Certifique-se de fornecer uma nota para que os usuários saibam que as legendas estão disponíveis para o vídeo.

Se você precisar usar legendas abertas, incorpore o texto à faixa de vídeo. Esse método é obtido com aplicativos de edição de vídeo que permitem a sobreposição de títulos no vídeo.

#### Mais informações - Legendas (pré-gravadas) (1.2.2)    {#more-information-captions-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html):
* [Como cumprir o Critério de sucesso 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#time-based-media)
* [W3C: Multimídia sincronizada](https://www.w3.org/AudioVideo/)
* [Legendas, transcrições e descrições de áudio - pelo WebAIM](https://webaim.org/techniques/captions/)

### Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3)    {#audio-description-or-media-alternative-pre-recorded}

* Critério de Sucesso 1.2.3
* Nível A
* Descrição de áudio ou alternativa de mídia (pré-gravada): Uma alternativa para mídia com base no tempo ou descrição de áudio do conteúdo de vídeo pré-gravado é fornecida para a mídia sincronizada, exceto quando a mídia é uma alternativa de mídia para texto e é claramente identificada como tal.

#### Propósito - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3)    {#purpose-audio-description-or-media-alternative-pre-recorded}

Os indivíduos cegos ou com deficiências visuais enfrentam barreiras de acessibilidade se as informações em um vídeo ou uma animação forem fornecidas apenas visualmente. Ou, se a trilha sonora não fornecer informações suficientes para permitir a compreensão do que está acontecendo visualmente.

#### Como cumprir - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3)    {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

Há duas abordagens que podem ser adotadas para atender a esse critério de sucesso. Ambas são aceitáveis:

1. Inclua uma descrição de áudio adicional para o conteúdo do vídeo. Você pode realizar essa abordagem de uma das três maneiras:

   * Durante as pausas na caixa de diálogo existente, forneça informações sobre as alterações na cena que não são apresentadas como parte da faixa de áudio existente;
   * Forneça uma faixa de áudio nova, adicional e opcional contendo a trilha sonora original, mas incluindo também informações de áudio extras sobre as mudanças no cenário.

      * Os usuários podem alternar entre a faixa de áudio existente (que *não* contém uma descrição de áudio) e a nova faixa de áudio (que *does* contém uma descrição de áudio).
      * Esse método evita a interrupção para usuários que não precisam de uma descrição adicional.
   * Crie uma segunda versão do conteúdo de vídeo para permitir descrições de áudio estendidas. Isso reduz as dificuldades associadas ao fornecimento de descrições de áudio detalhadas dentro das lacunas entre o diálogo existente, pausando temporariamente o áudio e o vídeo em pontos apropriados. Como resultado, uma descrição de áudio muito mais longa pode ser fornecida, antes que a ação inicie novamente. Como no exemplo anterior, essa é a melhor opção fornecida como uma faixa de áudio extra opcional para evitar a interrupção para usuários que não precisam de descrição adicional.


1. Forneça uma transcrição de texto que seja um equivalente de texto adequado dos elementos visuais e de áudio do vídeo ou da animação. Ela deve incluir, quando apropriado, uma indicação de quem está falando, uma descrição do cenário, expressões vocais. Dependendo da duração, é possível colocar a transcrição na mesma página que o vídeo ou a animação, ou em uma página separada; se você escolher a última opção, forneça um link para a transcrição ao lado do vídeo ou da animação.

Detalhes exatos de como criar um vídeo descrito por áudio estão fora do escopo deste guia. A criação de descrições de vídeo e áudio pode ser demorada, mas outros produtos da Adobe podem ajudar a realizar essas tarefas. Se você criar o conteúdo no Adobe Flash Professional, também será necessário criar um script para solicitar que o usuário baixe o plug-in adequado e fornecer uma alternativa em texto por meio do elemento `<noscript>`.

#### Mais informações - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html):
* [Como cumprir o Critério de sucesso 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://helpx.adobe.com/premiere-pro/using/whats-new.html)

### Legendas (ao vivo) (1.2.4)        {#captions-live}

* Critério de sucesso 1.2.4
* Nível AA
* Legendas (ao vivo): são fornecidas legendas para todo o conteúdo de áudio ao vivo na mídia sincronizada.

#### Propósito - Legendas (ao vivo) (1.2.4)       {#purpose-captions-live}

Esse critério de sucesso é idêntico às [Legendas (pré-gravadas)](#captions-pre-recorded), já que aborda as barreiras de acessibilidade enfrentadas pelos indivíduos surdos ou com deficiências auditivas, exceto que esse critério de sucesso lida com as apresentações ao vivo, como webcasts.

#### Como cumprir - Legendas (ao vivo) (1.2.4) {#how-to-meet-captions-live}

Siga as orientações fornecidas para [Legendas (pré-gravadas)](#captions-pre-recorded) acima. No entanto, devido à natureza ao vivo da mídia, a disposição da legenda tem de ser criada o mais rápido possível e em resposta ao que está acontecendo. Portanto, você deve considerar o uso de legendagem em tempo real ou ferramentas de voz para texto.

Instruções detalhadas estão além do escopo desse documento, mas os seguintes recursos disponibilizam informações úteis:

* [WebAIM: legendagem em tempo real](https://webaim.org/techniques/captions/realtime)
* [AccessIT (University of Washington): as legendas podem ser geradas automaticamente usando reconhecimento de voz?](https://www.washington.edu/doit/programs/accessit?1209)

#### Mais informações - Legendas (ao vivo) (1.2.4)    {#more-information-captions-live}

* [Noções sobre o Critério de sucesso 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [Como cumprir o Critério de sucesso 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-real-time-captions)

### Descrição de áudio (pré-gravado) (1.2.5)        {#audio-description-pre-recorded}

* Critério de Sucesso 1.2.5
* Nível AA
* Descrição de áudio (pré-gravado): A descrição de áudio é fornecida para todo o conteúdo de vídeo pré-gravado na mídia sincronizada.

#### Propósito - Descrição de áudio (pré-gravado) (1.2.5)    {#purpose-audio-description-pre-recorded}

Esse critério de sucesso é idêntico à [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-pre-recorded), exceto que os autores devem fornecer uma descrição de áudio muito mais detalhada para estar em conformidade com o Nível AA.

#### Como cumprir - Descrição de áudio (pré-gravado) (1.2.5)    {#how-to-meet-audio-description-pre-recorded}

Siga as orientações fornecidas para a [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-pre-recorded).

#### Mais informações - Descrição de áudio (pré-gravado) (1.2.5)    {#more-information-audio-description-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [Como cumprir o Critério de sucesso 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-audio-desc-only)

### Adaptável (1.3)       {#adaptable}

[Diretriz adaptável 1.3: Crie conteúdo que possa ser apresentado de diferentes maneiras (por exemplo, um layout mais simples) sem perder as informações ou a estrutura.](https://www.w3.org/TR/WCAG20/#content-structure-separation)

Esta diretriz abrange os requisitos necessários para apoiar as pessoas que:

* não poderá acessar as informações apresentadas por um autor em um *padrão* layout bidimensional, de várias colunas, colorido da página da Web

* usam uma exibição visual alternativa ou apenas de áudio, como um texto grande ou contraste alto.

### Informações e Relações (1.3.1)          {#info-and-relationships}

* Critério de Sucesso 1.3.1
* Nível A
* Informações e Relações: As informações, a estrutura e os relacionamentos transmitidos por meio da apresentação podem ser determinadas de forma programática ou estão disponíveis no texto.

#### Propósito - Informações e Relações (1.3.1)       {#purpose-info-and-relationships}

Muitas tecnologias de assistência utilizadas por pessoas com deficiência contam com informações estruturais para exibir ou produzir conteúdo de forma eficaz. Essas informações estruturais podem assumir a forma de cabeçalhos de página, linhas de tabela e cabeçalhos de coluna e tipos de lista. Por exemplo, um leitor de tela pode permitir que um usuário navegue por uma página de cabeçalho em cabeçalho. No entanto, quando o conteúdo da página parece ter estrutura apenas por meio de um estilo visual, em vez do HTML subjacente, então não há informações estruturais disponíveis para as tecnologias de assistência, limitando sua capacidade de suportar uma navegação mais fácil.

Esse critério de sucesso existe para garantir que essas informações estruturais sejam fornecidas por meio do HTML, para que os navegadores e as tecnologias de assistência possam acessar e aproveitar as informações.

#### Como cumprir - Informações e Relações (1.3.1)     {#how-to-meet-info-and-relationships}

O AEM facilita a criação de páginas da Web usando os elementos de HTML adequados. Abra o conteúdo da página no RTE (um componente de Texto) e use o **Formato** para especificar o elemento estrutural adequado (por exemplo, parágrafo e cabeçalho).

A imagem a seguir mostra o texto que foi estilizado como texto do parágrafo; a exibição do código-fonte que está sendo usada mostra que ela tem a abertura e o fechamento corretos &lt;p> e &lt;/p> tags.

![Um exemplo do elemento Parágrafo mostrado no modo de edição de origem (interface clássica).](assets/chlimage_1-18a.png)

Certifique-se de que as suas páginas da Web tenham a estrutura apropriada ao:

* **Utilização de cabeçalhos:**  

Desde que tenha os recursos de acessibilidade do RTE habilitados (consulte [AEM e acessibilidade](/help/sites-administering/rte-accessible-content.md)), o AEM oferece três níveis de cabeçalho de página. É possível usá-los para identificar seções e subseções de conteúdo. O cabeçalho 1 é o nível mais alto, o Cabeçalho 3 o mais baixo. O administrador do sistema pode configurar o sistema para permitir o uso de mais níveis de cabeçalho.

A imagem a seguir demonstra um exemplo dos diferentes tipos de cabeçalhos.

![Os cabeçalhos H1 até H3 são exibidos no seletor suspenso (interface clássica).](assets/chlimage_1-19a.png)

* **Texto destacado**:

Use o elemento  ou para indicar ênfase. Não use os cabeçalhos para destacar o texto dentro dos parágrafos.

    * Destaque o texto que deseja enfatizar;
    * Clique no ícone **B** (para &amp;lt;strong&amp;gt;) ou no ícone **I** (para &amp;lt;em&amp;gt;) mostrado no painel **Propriedades** (certifique-se de que o HTML esteja selecionado).

>[!NOTE]
>
>O RTE em uma instalação padrão do AEM está configurado para usar:
>
>* &lt;b> para &lt;strong>
* &lt;i> para &lt;em>
  >
Eles são efetivamente os mesmos, mas e são preferíveis, pois são html semanticamente corretos. Sua equipe de desenvolvimento pode configurar o RTE para usar e (em vez de e ), ao desenvolver a instância do projeto.

* **Use listas**: você pode usar o HTML para especificar três diferentes tipos de listas:

   * O `<ul>` é usado para *unordered* listas (com marcadores). Os itens da lista individual são identificados usando o elemento `<li>`. 

   no RTE, use o **Lista com marcadores** ícone .

   * O elemento `<ol>` é usado para as listas *numeradas*. Os itens da lista individual são identificados usando o elemento `<li>`. 

   No RTE, use o ícone **Lista numerada**.

Se desejar alterar o conteúdo existente em um tipo de lista específica, destaque o texto e selecione o tipo de lista apropriado. Como no exemplo anterior que mostra como o texto do parágrafo é inserido, os elementos da lista apropriados são adicionados automaticamente ao seu HTML, mas você pode visualizá-los na exibição da edição da fonte.

>[!NOTE]
O `<dl>` O RTE não oferece suporte para o elemento .

* **Usar tabelas**:

As tabelas de dados devem ser identificadas usando os elementos da tabela de HTML:

    * one `&lt;table>elemento `
    * a &quot;&lt;tr>elemento ` para cada linha da tabela
    * a &quot;&lt;th>elemento ` para cada linha e cabeçalho da coluna
    * a &quot;&lt;td>elemento ` para cada célula de dados

>[!NOTE]
As tabelas devem ser realizadas com a variável **Tabela** componente. Embora as tabelas possam ser criadas no componente Texto , isso não é recomendado.

Além disso, tabelas acessíveis usam os seguintes elementos e atributos:

    * O &quot;&lt;caption>O elemento ` é usado para fornecer uma legenda visível para a tabela. As legendas por padrão são exibidas de forma centralizada acima da tabela, mas podem ser posicionadas adequadamente usando o CSS. A legenda é associada à tabela de forma programática, portanto, é um método útil para fornecer uma introdução ao conteúdo.
    * O &quot;&lt;h3 class=&quot;summary&quot;>O elemento ` auxilia os usuários com deficiências visuais a compreender de forma mais fácil as informações apresentadas em uma tabela, fornecendo um resumo do que pode ser visto. Isso é particularmente útil quando layouts complexos ou não convencionais são usados (esse atributo não é exibido no navegador, somente é lido nas tecnologias de assistência).
    * O atributo &quot;scope&quot; do &quot;&lt;th>O elemento ` é usado para indicar se uma célula representa um cabeçalho de uma linha ou de uma coluna específica. Uma abordagem semelhante é a de usar o cabeçalho e os atributos de id em tabelas complexas, onde as células de dados podem ser associadas a um ou mais cabeçalhos.

>[!NOTE]
Por padrão, esses elementos e atributos não estão diretamente disponíveis, embora o administrador do sistema possa adicionar o suporte para esses valores na caixa de diálogo **Propriedades da tabela** (consulte [Adicionar suporte para outros elementos e atributos de HTML](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

Ao adicionar uma **Tabela**, você pode configurar **Propriedades da tabela** usando a caixa de diálogo .

    * uma **Legenda** apropriada.
    * Remova qualquer valor padrão para **Largura**, **Altura**, **Borda**, **Preenchimento da célula**, **Espaçamento entre células**. já que essas propriedades podem ser definidas em uma planilha de estilos global.

![Caixa de diálogo Propriedades da tabela.](assets/chlimage_1-20a.png)

Em seguida, você pode usar o **Propriedades da célula** para escolher se a célula é uma célula de dados ou de cabeçalho e, se for uma célula de cabeçalho, se está relacionada a uma linha ou coluna ou ambos:

![Caixa de diálogo Propriedades da chamada; definir uma linha (geralmente a primeira) como uma linha de cabeçalho.](assets/chlimage_1-21a.png)

* **Tabelas de dados complexos:**

Às vezes, quando há tabelas complexas com dois ou mais níveis de cabeçalhos, as Propriedades da tabela básicas podem não ser suficientes para fornecer toda a informação estrutural necessária. Para esses tipos de tabelas complexas, relações diretas devem ser criadas entre os cabeçalhos e suas células relacionadas usando o **header** e **id** atributos. Por exemplo, na tabela abaixo os cabeçalhos e IDs são combinados para fazer uma associação programática para usuários de tecnologia assistiva.

>[!NOTE]
O atributo id não está disponível em uma instalação predefinida. Ele pode ser ativado configurando regras de HTML e o serializador no RTE.

>[!NOTE]
As tabelas devem ser realizadas com a variável **Tabela** componente. Embora as tabelas possam ser criadas no componente Texto , isso não é recomendado.

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

Para fazer isso no AEM, você deve adicionar a marcação diretamente usando o modo de edição da fonte.

>[!NOTE]
Essa funcionalidade não está imediatamente disponível em uma instalação padrão. Requer a configuração do RTE; regras de HTML e serializador.

#### Mais informações - Informações e Relações (1.3.1) {#more-information-info-and-relationships}

* [Noções sobre o Critério de sucesso 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [Como cumprir o Critério de sucesso 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-programmatic)

### Características sensoriais (1.3.3)        {#sensory-characteristics}

* Critério de Sucesso 1.3.3
* Nível A
* Características sensoriais: as instruções fornecidas para compreender e utilizar o conteúdo não dependem somente das características sensoriais dos componentes, como forma, tamanho, localização visual, orientação ou som.

#### Propósito - Características sensoriais (1.3.3)       {#purpose-sensory-characteristics}

Ao apresentar as informações, os designers geralmente se concentram nos recursos de design visual, como cor, forma, estilo de texto ou a posição relativa/absoluta de uma parte do conteúdo. Essas podem ser técnicas avançadas de design na transmissão de informações, mas os indivíduos cegos ou com deficiências visuais podem não conseguir acessar as informações que exigem a identificação visual de atributos como posição, cor ou forma.

Da mesma forma, as informações que exigem a distinção entre sons diferentes (por exemplo, conteúdo falado masculino ou feminino) apresentam barreiras de acessibilidade para os indivíduos com deficiência auditiva, se não estiverem refletidas em nenhuma alternativa em texto para o conteúdo de áudio.

>[!NOTE]
Para os requisitos relacionados às alternativas de cor, consulte [Uso de cor](#use-of-color).

#### Como cumprir - Características sensoriais (1.3.3)       {#how-to-meet-sensory-characteristics}

Certifique-se de que todas as informações que dependem das características visuais do conteúdo da página também sejam apresentadas em um formato alternativo.

* Não se baseie na posição visual para fornecer informações. Por exemplo, se você deseja fazer uma referência para os usuários sobre um menu no lado direito da página para obter acesso a mais informações, não consulte *no menu à direita*; em vez disso, nomeie o menu (por exemplo, por meio de um cabeçalho) e faça referência a esse nome no texto.
* Não se baseie no estilo do texto (por exemplo, negrito ou itálico) como a única maneira de transmitir as informações.

>[!NOTE]
A utilização de termos descritivos é aceitável se estes forem entendidos como relevantes em um contexto não visual. Por exemplo, usando *above* e *below* geralmente seria aceitável, pois implicam, respectivamente, conteúdo antes e depois de um item específico de conteúdo. Ainda faria sentido quando o conteúdo fosse falado em voz alta.

#### Mais informações - Características sensoriais (1.3.3)       {#more-information-sensory-characteristics}

* [Noções sobre o Critério de sucesso 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [Como cumprir o Critério de sucesso 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-understanding)

### Discernível (1.4)       {#distinguishable}

[Diretriz 1.4 Discernível: facilitar a visualização e a audição de conteúdos aos usuários, incluindo a separação do primeiro plano e do plano de fundo. ](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### Utilização de cor (1.4.1)              {#use-of-color}

* Critério de Sucesso 1.4.1
* Nível A
* Utilização de cor: A cor não é usada como o único meio visual de transmitir informações, indicar uma ação, solicitar uma resposta ou distinguir um elemento visual.

>[!NOTE]
Esse critério de sucesso aborda especificamente a percepção da cor. Outras formas de percepção são abordadas na [Adaptável (1.3)](#adaptable); incluindo acesso programático a cores e outras codificações de apresentação visual.

#### Propósito - Utilização de cor (1.4.1)       {#purpose-use-of-color}

A cor é uma maneira eficaz de aprimorar o apelo estético das páginas da Web e também é útil na transmissão de informações. No entanto, há uma série de deficiências visuais, da cegueira à daltonismo, o que significa que algumas pessoas não conseguem distinguir entre certas cores. Esse problema torna o código de cores uma maneira não confiável de fornecer informações.

Por exemplo, alguém com daltonismo não consegue distinguir entre tons de verde e vermelho. Eles podem ver as duas cores como uma terceira cor (por exemplo, marrom), nesse caso, eles não conseguem distinguir entre vermelho, verde e marrom.

Além disso, a cor não pode ser percebida por pessoas que usam navegadores somente de texto, dispositivos de exibição monocromáticos ou que visualizam uma impressão em preto-e-branco da página.

#### Como cumprir - Utilização de cor (1.4.1)       {#how-to-meet-use-of-color}

Sempre que a cor for usada para transmitir informações, certifique-se de que a informação está disponível, sem a necessidade da visualização das cores.

Por exemplo, verifique se as informações fornecidas através das cores também estão evidentes no texto. A ilustração abaixo mostra como a cor e o texto indicam a disponibilidade de assentos para uma performance:

<table>
 <tbody>
  <tr>
   <td><p><strong>Desempenho</strong></p> </td>
   <td><p><strong>Disponibilidade</strong></p> </td>
  </tr>
  <tr>
   <td><p>Terça-feira, 16 de março<sup>th</sup></p> </td>
   <td><p>LUGARES DISPONÍVEIS</p> </td>
  </tr>
  <tr>
   <td><p>Quarta-feira, 17 de março<sup>th</p> </td>
   <td><p>LUGARES DISPONÍVEIS</p> </td>
  </tr>
  <tr>
   <td><p>Quinta-feira, 18 de março<sup>th</sup></p> </td>
   <td><p>VENDIDO</p> </td>
  </tr>
 </tbody>
</table>

Se a cor for usada como dica para fornecer informações, você deve fornecer uma dica visual extra, como alterar o estilo (por exemplo, negrito, itálico) ou a fonte. Isso ajuda os indivíduos com problemas de visão ou daltonismo a identificar as informações. No entanto, não é possível depender dessas opções completamente, pois não ajuda os indivíduos que não conseguem visualizar nada na página.

#### Mais informações - Utilização de cor (1.4.1) {#more-information-use-of-color}

* [Noções sobre o Critério de sucesso 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Como cumprir o Critério de sucesso 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Orientação sobre como atender a uma relação de contraste de 3:1, com uma lista de cores &quot;seguras para usar na Web&quot;](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### Contraste (Mínimo) (1.4.3)       {#contrast-minimum}

* Critério de Sucesso 1.4.3
* Nível AA
* Contraste (Mínimo): A apresentação visual de texto e imagens de texto tem uma relação de contraste de pelo menos 4.5:1, exceto para o seguinte:

   * Texto grande: O texto em grande escala e as imagens de texto em grande escala têm uma relação de contraste de pelo menos 3:1.
   * Incidental: o texto ou as imagens de texto que fazem parte de um componente de interface de usuário inativo, que são meramente decorativos, e não estão visíveis para ninguém ou que são parte de uma imagem que inclui outro conteúdo visual significativo, não têm requisito de contraste.
   * Logotipos: o texto que faz parte de um logotipo ou marca comercial não tem requisito de contraste.

#### Propósito - Contraste (Mínimo) (1.4.3)       {#purpose-contrast-minimum}

Os indivíduos com certas deficiências visuais podem não conseguir distinguir entre determinados pares de cores de baixo contraste. Problemas de acessibilidade podem ocorrer para essas pessoas se:

* O texto contrasta mal com a cor de fundo.
* A codificação de cores do texto (como o texto do link e o texto sem link) é importante na distinção das informações.

>[!NOTE]
O texto usado exclusivamente para fins decorativos está excluído desse critério de sucesso.

#### Como cumprir - Contraste (Mínimo) (1.4.3)       {#how-to-meet-contrast-minimum}

Verifique se o texto contrasta o suficiente com o plano de fundo. As relações de contraste dependem do tamanho e do estilo do texto em questão:

* Para texto com menos de 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste entre o texto/imagens de texto e o plano de fundo deve ser, pelo menos, 4.5:1.
* Para texto com pelo menos 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste deve ser de pelo menos 3:1.
* Se um plano de fundo for estampado, o plano de fundo ao redor de qualquer texto deverá ser sombreado para que a proporção 4.5:1 ou 3:1 seja mantida.

Para verificar as relações de contraste, use uma ferramenta de contraste em cores, como [Analisador de contraste de cores do grupo Paciello](https://www.paciellogroup.com/resources/contrast-analyser.html) ou [Verificador de contraste de cores do WebAIM](https://webaim.org/resources/contrastchecker/). Essas ferramentas permitem verificar pares de cores e relatar quaisquer problemas de contraste.

Como alternativa, se você estiver menos preocupado sobre como especificar a aparência de sua página, poderá optar por não especificar as cores do texto de plano de fundo e de primeiro plano. Nenhuma verificação de contraste é necessária, pois o navegador do usuário determina as cores do texto e do plano de fundo.

Se não for possível atender aos níveis de contraste recomendados, forneça um link para uma versão alternativa equivalente da página (que não tenha problemas de contraste de cores). Ou permita que o usuário ajuste o contraste do esquema de cores da página de acordo com suas próprias necessidades.

#### Mais informações - Contraste (Mínimo) (1.4.3)       {#more-information-contrast-minimum}

* [Noções sobre o Critério de sucesso 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [Como cumprir o Critério de sucesso 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-visual-audio-contrast-contrast)

### Imagens de texto (1.4.5)    {#images-of-text}

* Critério de Sucesso 1.4.5
* Nível AA
* Imagens de texto: se as tecnologias usadas puderem obter a apresentação visual, o texto será usado para transmitir as informações, em vez das imagens de texto, exceto para o seguinte:

   * Personalizável: A imagem do texto pode ser visualmente personalizada de acordo com as necessidades do usuário;
   * Essencial: Uma apresentação específica do texto é essencial para a transmissão das informações.

>[!NOTE]
Os logotipos (texto que faz parte de um logotipo ou marca comercial) são considerados essenciais.

#### Propósito - Imagens de texto (1.4.5)       {#purpose-images-of-text}

Imagens de texto são usadas com frequência quando um determinado estilo de texto é preferido; por exemplo, um logotipo ou se o texto foi gerado de outra fonte (por exemplo, uma digitalização de um documento em papel). No entanto, em comparação com o texto apresentado no HTML e o estilo usando CSS, as imagens de texto não têm flexibilidade para alterar o tamanho ou a aparência, o que pode ser necessário para os indivíduos com deficiência visual ou dificuldade de leitura.

#### Como cumprir - Imagens de texto (1.4.5)       {#how-to-meet-images-of-text}

Se as imagens de texto tiverem que ser utilizadas, use o CSS para substituir as imagens de texto pelo texto equivalente em HTML, para que o texto seja disponibilizado de forma personalizada. Para ver um exemplo, consulte [C30: Uso de CSS para substituir texto por imagens de texto e fornecer controles de interface do usuário para alternar](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Mais informações - Imagens de texto (1.4.5)       {#more-information-images-of-text}

* [Noções sobre o Critério de sucesso 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [Como cumprir o Critério de sucesso 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-visual-audio-contrast-text-presentation)

## Princípio 2: operável       {#principle-operable}

[Princípio 2: operável - os componentes da interface de usuário e a navegação precisam ser operáveis.](https://www.w3.org/TR/WCAG20/#operable)

### Pausar, Interromper, Ocultar (2.2.2)        {#pause-stop-hide}

* Critério de Sucesso 2.2.2
* Nível A
* Pausar, Interromper, Ocultar: para mover, piscar, deslocar ou atualizar automaticamente as informações, as seguintes opções são verdadeiras:

   * Mover, piscar, deslocar: Para qualquer informação móvel, piscando ou rolando que (a) começa automaticamente, (b) dura mais de cinco segundos e (c) seja apresentada em paralelo com outro conteúdo, há um mecanismo para o usuário pausar, parar ou ocultá-la, a menos que o movimento, piscar ou rolar seja parte de uma atividade essencial;
   * Atualização automática: Para qualquer atualização automática de informações que (a) é iniciada automaticamente e (b) é apresentada em paralelo com outro conteúdo, há um mecanismo para o usuário pausar, interromper ou ocultar ou controlar a frequência da atualização, a menos que a atualização automática faça parte de uma atividade em que é essencial.

Os pontos a serem observados são:

1. Para os requisitos relacionados ao conteúdo piscante ou piscante, consulte [Não criar o conteúdo em uma forma conhecida por causar convulsões (2.3)](#seizures).
1. Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário de utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte [Requisito de conformidade 5: Não interferência](https://www.w3.org/TR/WCAG20/#cc5).
1. O conteúdo que é atualizado periodicamente pelo software ou que é transmitido ao agente do usuário não é obrigado a preservar ou apresentar as informações geradas ou recebidas entre o início da pausa e a retomada da apresentação, pois isso pode não ser tecnicamente possível e, em muitas situações, pode ser enganador.
1. Uma animação que ocorre como parte de uma fase de pré-carregamento ou uma situação semelhante pode ser considerada essencial se a interação não puder ocorrer durante essa fase para todos os usuários, e se não indicar o progresso, poderá confundir os usuários ou fazer com que eles pensem que o conteúdo foi congelado ou quebrado.

#### Propósito - Pausar, Interromper, Ocultar (2.2.2)       {#purpose-pause-stop-hide}

Alguns usuários podem achar que o conteúdo que se move é perturbador e dificulta a concentração em outras partes da página. Além disso, esse conteúdo pode ser de difícil leitura para as pessoas que têm problemas para acompanhar o texto em movimento.

#### Como cumprir - Pausar, Interromper, Ocultar (2.2.2)       {#how-to-meet-pause-stop-hide}

Dependendo da natureza do conteúdo, você pode aplicar uma ou mais das seguintes sugestões ao criar páginas da Web com conteúdo móvel, piscante ou intermitente:

* Forneça um meio de pausar o deslocamento do conteúdo para que os usuários tenham tempo suficiente para lê-lo. Por exemplo, painéis de notícias ou um texto atualizado automaticamente.
* Verifique se o conteúdo em modo intermitente é interrompido após cinco segundos.
* Use as tecnologias adequadas para exibir um conteúdo em modo intermitente que possa ser desativado pelo navegador. Por exemplo, os arquivos Graphics Interchange Format (GIF) ou Animated Portable Network Graphics (APNG).
* Forneça um controle de formulário na página da Web para permitir que o usuário desative todo o conteúdo em modo intermitente da página.
* Se nenhuma das situações anteriores for possível, forneça um link para uma página que contenha todo o conteúdo, mas sem piscar.

#### Mais informações - Pausar, Interromper, Ocultar (2.2.2)     {#more-information-pause-stop-hide}

* [Noções sobre o Critério de sucesso 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [Como cumprir o Critério de sucesso 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-time-limits-pause)

### Convulsões (2.3)    {#seizures}

[Diretriz Convulsões 2.3: não crie o conteúdo em uma forma conhecida por causar convulsões](https://www.w3.org/TR/WCAG20/#seizure)

### Três flashes ou abaixo do limite (2.3.1)    {#three-flashes-or-below-threshold}

* Critério de Sucesso 2.3.1
* Nível A
* Três Flashes ou Abaixo do limite: As páginas da Web não contêm nada que pisque mais de três vezes em um período de um segundo ou o flash está abaixo dos limites de flash geral e flash vermelho.

>[!NOTE]
Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário de utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte [Requisito de conformidade 5: Não interferência](https://www.w3.org/TR/WCAG20/#cc5).

#### Finalidade - Três flashes ou Abaixo do limite (2.3.1) {#purpose-three-flashes-or-below-threshold}

Em certos casos, o conteúdo em modo flash pode causar convulsões fotossensíveis. Esse critério de sucesso permite que esses usuários acessem e acessem todo o conteúdo sem se preocupar com o conteúdo com flashes.

#### Como cumprir - Três flashes ou Abaixo do limite (2.3.1)       {#how-to-meet-three-flashes-or-below-threshold}

Siga as etapas abaixo para garantir que as seguintes técnicas sejam aplicadas:

* Assegurar que os componentes não pisquem mais de três vezes durante um período de um segundo;
* Se a condição acima não puder ser cumprida, exibir o conteúdo em modo flash em uma *área segura pequena* em pixels na tela. Essa área é calculada por meio de uma fórmula complexa, abordada em [G176: Manter a área de flashes suficientemente pequena](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), portanto, essa técnica só deve ser seguida se o conteúdo em modo flash for necessário.

#### Mais informações - Três flashes ou Abaixo do limite (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Noções sobre o Critério de sucesso 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [Como cumprir o Critério de sucesso 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#seizure)

### Página com título (2.4.2)        {#page-titled}

* Critério de Sucesso 2.4.2
* Nível A
* Página com título: As páginas da Web têm títulos que descrevem tópico ou propósito.

#### Finalidade - Página com título (2.4.2)       {#purpose-page-titled}

Esse critério de sucesso ajuda todos, independentemente de qualquer incapacidade cognitiva, a identificar rapidamente o conteúdo de uma página da Web sem precisar ler a página na íntegra. Esse design é útil quando várias páginas da Web são abertas em guias do navegador, já que o título da página é mostrado na guia e, portanto, pode ser localizado rapidamente.

#### Como cumprir - Página com título (2.4.2)       {#how-to-meet-page-titled}

Quando uma nova página HTML é criada no AEM, é possível especificar o título da página. Certifique-se de que o título descreva adequadamente o conteúdo da página, para que os visitantes possam identificar rapidamente se o conteúdo é relevante para suas necessidades.

Também é possível editar o título da página ao editar uma página, que pode ser acessada por **Sidekick** - **Página** guia - **Propriedades da Página...**

#### Mais informações - Página com título (2.4.2) {#more-information-page-titled}

* [Noções sobre o Critério de sucesso 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [Como cumprir o Critério de sucesso 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-title)

### Finalidade do link (em contexto) (2.4.4)        {#link-purpose-in-context}

* Critério de Sucesso 2.4.4
* Nível A
* Finalidade do link (em contexto): A finalidade de cada link pode ser determinada somente pelo texto do link ou pelo texto do link, juntamente com o contexto do link determinado de forma programática. A exceção é quando a finalidade do link é ambígua para os usuários em geral.

#### Finalidade - Finalidade do link (Em contexto) (2.4.4)       {#purpose-link-purpose-in-context}

Para todos os usuários, independentemente da incapacidade cognitiva, é essencial indicar claramente a direção de um link por meio de um texto de link apropriado. Esse design ajuda os usuários a decidir se querem realmente seguir um link. Para usuários deficientes visuais, um texto de link significativo é útil quando há vários links em uma página (principalmente se a página tiver excesso de texto), já que um texto de link significativo fornece uma indicação mais clara da funcionalidade da página de destino. Embora os usuários de tecnologias assistivas, que podem gerar uma lista de todos os links em uma única página, possam entender mais facilmente o texto do link fora de contexto.

#### Como cumprir - Finalidade do link (Em contexto) (2.4.4)     {#how-to-meet-link-purpose-in-context}

Acima de tudo, verifique se a finalidade de um link está claramente descrita no texto.

* Exemplo incorreto:

   * Texto: Para obter detalhes sobre aulas noturnas no segundo trimestre de 2010, clique aqui.
   * Motivo: não indica clara e inequivocamente o seu destino.

* Exemplo correto:

   * Texto: aulas à noite para o segundo trimestre de 2010 - mais informações.
   * Motivo: Ajustando ligeiramente o texto e a posição do elemento de link, o texto do link pode ser melhorado:

Os links devem ser redigidos de forma consistente ao longo das páginas, principalmente em barras de navegação. Por exemplo, se um link para uma página específica for chamado de **Publicações** em uma página, use esse termo nas outras páginas para garantir a consistência.

No entanto, no momento da escrita, há algumas questões relacionadas ao uso de títulos:

* O texto contido no atributo de título só está disponível para usuários do mouse como um pop-up de dica de ferramenta e não pode ser acessado usando o teclado.
* Os leitores de tela podem ler atributos de título, mas essa funcionalidade pode não ser ativada por padrão; dessa forma, os usuários podem não estar cientes de que existe um atributo de título.
* É difícil alterar a aparência do texto do título, o que significa que pode ser difícil ou impossível de ler por algumas pessoas.

Portanto, embora o atributo de título possa ser usado para fornecer contexto extra a um link, esteja ciente de suas limitações e não o use como uma alternativa ao texto de link apropriado.

Sempre que um link for constituído por uma imagem, certifique-se de que o texto alternativo da imagem descreva o destino do link. Por exemplo, se uma imagem de uma estante de livros for definida como um link para as publicações de uma pessoa, o texto alternativo deverá informar **Publicações de John Smith**, e não **Estante de livros**.

Como alternativa, se a âncora do link contiver texto que descreve a finalidade do link, além do elemento de imagem (e, portanto, o texto aparece ao lado da imagem), use um atributo alternativo vazio para a imagem:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
O trecho acima é uma ilustração, é recomendável usar a variável **Imagem** componente.

Embora seja aconselhável fornecer um texto de link que identifique a finalidade do link sem a necessidade de contexto adicional, reconhece-se que isto nem sempre é possível. Link contextuais gratuitos podem ser usados nos casos a seguir, exemplos de HTML que podem ser encontrados em [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs).

* Sempre que o texto do link fizer parte de uma lista de links estritamente relacionados e quando um item de lista que delimita o link fornecer contexto suficiente.
* Sempre que a finalidade de um link puder ser claramente identificada no texto do parágrafo *anterior* (não o seguinte).
* Sempre que o link estiver contido em uma tabela de dados e, portanto, a finalidade puder ser claramente identificada nos cabeçalhos associados.
* Sempre que uma lista de links estiver contida em um conjunto de cabeçalhos e o próprio cabeçalho fornecer o contexto adequado.
* Sempre que uma lista de links estiver contida em um link aninhado e o item da lista principal acima do link aninhado fornecer o contexto adequado.

Às vezes, quando há vários links em uma página (cada um dos quais fornece a direção de um link em detalhes complexos, mas necessários), pode ser apropriado fornecer uma versão alternativa da página da Web que exibe exatamente o mesmo conteúdo, mas onde o texto do link não é tão detalhado.

Como alternativa, os scripts podem ser usados de forma que uma quantidade mínima de texto seja fornecida dentro do próprio link. Mas ao ativar um controle apropriado posicionado na parte superior da página, o texto do link é *expandido* mais detalhadamente. Uma abordagem semelhante é usar o CSS para *ocultar* o link completo de usuários deficientes visuais, mas ainda o exibe na íntegra para os usuários de leitores de tela. Isso está fora do escopo deste documento, mas mais informações sobre como isso pode ser feito podem ser encontradas no relatório [Mais informações - Finalidade do link (em contexto) (2.4.4)](#more-information-link-purpose-in-context) seção.

#### Mais informações - Finalidade do link (no contexto) (2.4.4) {#more-information-link-purpose-in-context}

* [Noções sobre o Critério de sucesso 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs)
* [C7: utilizar CSS para ocultar uma parte do texto do link](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## Princípio 3: compreensível    {#principle-understandable}

[Princípio 3: compreensível - A informação e a operação da interface do usuário devem ser compreensíveis.](https://www.w3.org/TR/WCAG20/#understandable)

### Torne o conteúdo do texto legível e compreensível (3.1)       {#make-text-content-readable-and-understandable}

[Diretriz 3.1 Legível: tornar o conteúdo do texto legível e compreensível.](https://www.w3.org/TR/WCAG20/#meaning)

### Idioma da página (3.1.1)       {#language-of-page}

* Critério de Sucesso 3.1.1
* Nível A
* Idioma da página: O idioma humano padrão de cada página da Web pode ser determinado de forma programática.

#### Finalidade - Idioma da página (3.1.1)       {#purpose-language-of-page}

A finalidade deste critério de sucesso é garantir que o texto e outro conteúdo linguístico sejam apresentados corretamente. Para leitores de tela, isso garante que o conteúdo seja pronunciado corretamente, enquanto os navegadores visuais têm maior probabilidade de exibir determinados conjuntos de caracteres corretamente.

#### Como cumprir - Idioma da página (3.1.1)       {#how-to-meet-language-of-page}

Para cumprir este critério de sucesso, o idioma padrão de uma página da Web pode ser identificado usando o atributo `lang`dentro do elemento`<html>` no topo da página. Por exemplo:

* Se uma página for escrita em inglês britânico, o elemento `<html>` deverá informar:

`<html lang = "en-gb">`

* Para processar uma página como inglês dos EUA, deverá ser adotado o seguinte padrão:

`<html lang = "en-us">`

No AEM, o idioma padrão da sua página é definido ao criá-la, mas também pode ser alterado durante a edição de uma página, acessível em **Sidekick** - guia **Página** - **Propriedades da página...** - guia **Avançadas**.

#### Mais Informações - Idioma da Página (3.1.1) {#more-information-language-of-page}

* [Noções sobre o Critério de sucesso 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [Como cumprir o Critério de sucesso 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-meaning-doc-lang-id)
* Os códigos são baseados em ISO 639-1. Uma lista mais extensa de códigos para cada idioma pode ser encontrada no [Site W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de Partes (3.1.2)              {#language-of-parts}

* Critério de Sucesso 3.1.2
* Nível AA
* Idioma de Partes: O idioma humano de cada passagem ou frase do conteúdo pode ser determinado de forma programática, exceto para nomes próprios, termos técnicos, palavras de idioma indeterminado e palavras ou frases que se tornaram parte do vernáculo do texto imediatamente circundante.

#### Finalidade - Idioma de Partes (3.1.2)       {#purpose-language-of-parts}

A finalidade deste critério de sucesso é semelhante ao critério de sucesso de [Idioma da Página](#language-of-page), exceto que se aplica a páginas da Web com conteúdo em múltiplos idiomas em uma única página (por exemplo, devido a citações ou palavras incomuns).

As páginas que aplicam este critério de sucesso permitem:

* O software de transição Braille é usado para inserir caracteres acentuados.
* Leitores de tela para pronunciar corretamente as palavras que não estão no idioma padrão.
* Permitem que as ferramentas de tradução, como o Google Translate, traduzam corretamente o conteúdo de um idioma para outro.

#### Como Cumprir - Idioma de Partes (3.1.2)       {#how-to-meet-language-of-parts}

O `lang` pode ser usado para identificar alterações no idioma do conteúdo. Por exemplo, uma citação em alemão (ISO 639-1, código “de”) pode ser apresentada da seguinte maneira:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
Blocos de citação não são suportados em uma instância predefinida. Um componente personalizado pode ser desenvolvido para suportar o recurso.

Da mesma forma, o navegador poderá processar uma palavra incomum ou frase corretamente se o elemento `span` for usado da seguinte maneira:

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</span>.</p>
```

>[!NOTE]
Não é necessário seguir este critério de sucesso ao incluir nomes ou cidades em diferentes idiomas, ou ao usar palavras de empréstimo ou frases que se tornaram comuns no idioma padrão (como *schadenfreude* em inglês).

Para adicionar o elemento span, com um idioma apropriado, você pode editar manualmente a sua marcação HTML no modo de edição de fonte da RTE para ser exibido como acima. Como alternativa, o atributo `lang` pode ser incluído na RTE pelo administrador do sistema (consulte [Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Mais Informações - Idioma de Partes (3.1.2) {#more-information-language-of-parts}

* [Noções sobre o Critério de sucesso 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html)
* [Como cumprir o Critério de sucesso 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-meaning-other-lang-id)

### Ajude os usuários a evitar e corrigir erros (3.3)    {#help-users-avoid-and-correct-mistakes}

[Diretriz 3.3 Assistência de entrada: ajudar os usuários a evitar e corrigir erros](https://www.w3.org/TR/WCAG20/#minimize-error)

### Etiquetas ou Instruções (3.3.2)    {#labels-or-instructions}

* Critério de Sucesso 3.3.2
* Nível A
* Etiquetas ou Instruções: Rótulos ou instruções são fornecidas quando o conteúdo requer entrada do usuário.

#### Finalidade - Etiquetas ou Instruções (3.3.2)       {#purpose-labels-or-instructions}

Fornecer instruções para ajudar as pessoas a preencher formulários é uma parte fundamental das boas práticas de usabilidade da interface. É útil para pessoas com deficiências visuais ou cognitivas que de outra forma poderiam ter dificuldade para entender o layout de um formulário e o tipo de dados a serem fornecidos em um campo de formulário específico.

Em AEM, um rótulo padrão é adicionado quando você adiciona um componente de formulário, como um **Campo de texto**, à página. Esse título padrão depende do tipo de componente. Você pode adicionar seu próprio título na **Título e texto** da caixa de diálogo de edição desse campo. É importante garantir que os rótulos ajudem os usuários a entender os dados associados a cada componente do formulário.

![Guia Título e texto (caixa de diálogo Editar); o título &#39;Descrição&#39; foi adicionado.](assets/chlimage_1-22a.png)

Essa **Título** deve ser usado para elementos de campo, pois fornece um rótulo que está disponível para a tecnologia assistiva. Apenas escrever um rótulo no texto ao lado do campo não é suficiente.

Para alguns componentes de formulário, também é possível ocultar visualmente rótulos usando o **Ocultar Título** caixa de seleção. Rótulos ocultos dessa maneira ainda estão disponíveis para a tecnologia assistiva, mas não são exibidos na tela. Embora esta possa ser uma boa abordagem em algumas situações, é melhor incluir um rótulo visual sempre que possível. Alguns usuários podem estar olhando para uma pequena seção da tela (um campo por vez) e precisam de rótulos para identificar o campo corretamente.

#### Botões de imagem {#image-buttons}

Quando são utilizados botões de imagem (por exemplo, o componente **Botão de Imagem**), o campo **Título** na guia **Título e Texto** da janela de edição fornece o texto alternativo para a imagem, em vez da etiqueta. Assim, no exemplo abaixo, a imagem com o texto `Submit`tem o texto alternativo de `Submit`, adicionado usando o campo **Título** na janela de edição.

![Botão de imagem com o texto alternativo definido no campo Título (caixa de diálogo Editar).](assets/chlimage_1-23a.png)

#### Grupos de campos de formulário {#groups-of-form-fields}

Sempre que houver um grupo de controles relacionados, como **Grupo de opções**, um título pode ser necessário para o grupo e controles individuais. Ao adicionar um conjunto de botões de opção no AEM, o campo **Título** fornece esse título de grupo, enquanto títulos individuais são especificados conforme os botões de opção (**Itens**) são criados.

![Adicionar itens ao grupo de opções. O título do grupo é &quot;Entrar em contato por&quot; - definido no campo Título .](assets/chlimage_1-24a.png)

Contudo, não existe uma associação programática entre o título do grupo e os próprios botões de opção. Os editores de modelo devem vincular o título na `fieldset` e `legend` tags para criar essa associação, e isso só pode ser feito editando o código fonte da página. Alternativamente, um administrador do sistema pode adicionar suporte a esses elementos para que eles apareçam na janela **Propriedades do Campo** (consulte [Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Considerações adicionais para formulários {#additional-considerations-for-forms}

Se os dados devem ser inseridos em um formato específico, deixe isso claro no texto da etiqueta. Por exemplo, se uma data deve ser inscrita no formato `DD-MM-YYYY`, indique isso especificamente como parte da etiqueta. Isso significa que quando os usuários de leitores de tela encontrarem o campo, a etiqueta será anunciada automaticamente, juntamente com as informações adicionais sobre o formato.

Se a entrada de um campo de formulário for obrigatória, deixe isso claro usando a palavra &quot;obrigatório&quot; como parte do rótulo. O AEM adiciona um asterisco quando um campo é obrigatório, mas seria ideal incluir a palavra `required` na própria etiqueta (no campo **Título** na janela de edição).

![Adição de informações adicionais (a palavra &quot;obrigatório&quot;) para usuários de leitores de tela no campo &quot;Título&quot;.](assets/chlimage_1-25a.png)

O posicionamento dos rótulos também é importante, pois ajuda a localizar os campos apropriados. Isso é particularmente importante quando o usuário se depara com um formulário complexo. Siga a convenção abaixo:

* Caixas de seleção ou botões de opção:

Os rótulos são posicionados imediatamente à direita do campo.

* Todos os outros componentes do formulário (por exemplo, caixas de texto, caixas de combinação):

Os rótulos são posicionados imediatamente acima ou à esquerda do campo.

Em formulários simples, com funcionalidade limitada, rotule adequadamente uma `Submit` pode atuar como um rótulo para o campo adjacente (por exemplo, `Search`). Isso é útil em situações em que encontrar espaço para o texto da etiqueta pode ser difícil.

#### Mais Informações - Etiquetas ou Instruções (3.3.2)       {#more-information-labels-or-instructions}

* [Noções sobre o Critério de sucesso 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [Como cumprir o Critério de sucesso 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-minimize-error-cues)
