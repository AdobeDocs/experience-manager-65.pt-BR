---
title: 'Criação de conteúdo acessível (Conformidade com a WCAG 2.0)  '
seo-title: 'Criação de conteúdo acessível (Conformidade com a WCAG 2.0)  '
description: A WCAG 2.0 consiste em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável para pessoas com necessidades especiais.
seo-description: A WCAG 2.0 consiste em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável para pessoas com necessidades especiais.
page-status-flag: de-activated
uuid: c2c0cac0-2a9f-478d-8261-e8cc894aae34
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 378bc33d-ab6c-4651-9688-102c961561fc
translation-type: tm+mt
source-git-commit: af27ed32c21a338600201e05871c1b18548ecba6
workflow-type: tm+mt
source-wordcount: '9241'
ht-degree: 94%

---


# Criação de conteúdo acessível (Conformidade com o WCAG 2.0){#creating-accessible-content-wcag-conformance}

>[!CAUTION]
>
>Como a interface clássica foi substituída no AEM 6.4, o conteúdo desta página não foi atualizado para WCAG 2.1.
>
>Consulte as seguintes páginas para obter detalhes sobre o AEM e o WCAG 2.1:
>
>* [AEM e as diretrizes de acessibilidade da Web](/help/managing/web-accessibility.md)
>* [Um guia rápido para a WCAG 2.1](/help/managing/qg-wcag.md)
>* [Criação de conteúdo acessível (Conformidade com o WCAG 2.1)](/help/sites-authoring/creating-accessible-content.md)


A WCAG 2.0 consiste em um conjunto de diretrizes de tecnologia independentes e critérios de sucesso para ajudar a tornar o conteúdo da Web acessível e utilizável para pessoas com necessidades especiais.

>[!NOTE]
>
>Consulte também:
>
>* Nosso [Guia rápido do WCAG 2.0](/help/managing/qg-wcag.md) para obter mais detalhes
>* [Configurar o Editor de Rich Text para a produção de conteúdo acessível](/help/sites-administering/rte-accessible-content.md)
>



São classificados de acordo com os três níveis de conformidade: Nível A (o mais baixo), Nível AA e Nível AAA (o mais alto). Resumidamente, os níveis são definidos como apresentado a seguir:

* **Nível A**: o site atinge um nível mínimo básico de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A são cumpridos.
* **Nível AA:** é o nível ideal que deve ser alcançado, no qual o site atinge um nível superior de acessibilidade, para que seja acessível à maioria das pessoas, em grande parte das situações e usando a maioria das tecnologias. Para chegar a esse nível, todos os Critérios de sucesso de Nível A e Nível AA precisam ser cumpridos.
* **Nível AAA**: o site atinge um nível muito alto de acessibilidade. Para atingir esse nível, todos os Critérios de sucesso do Nível A, Nível AA e Nível AAA são cumpridos.

Ao criar o seu site, é necessário determinar o nível global com o qual você gostaria que ele estivesse em conformidade.

A seção a seguir apresenta as [Diretrizes da WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) com os critérios de sucesso relacionados aos [níveis de conformidade](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) A e AA.

>[!NOTE]
>
>Como não é possível cumprir todos os Critérios de sucesso de Nível AAA para certos tipos de conteúdo, não é recomendado que esse nível de conformidade seja exigido como uma política geral.

>[!NOTE]
>
>Nesse documento são usados:
>
>* os nomes curtos para as [Diretrizes da WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines).
>* a numeração usada nas [Diretrizes da WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) para auxiliar na referência cruzada com o site da WCAG.
>



## Princípio 1: perceptível    {#principle-perceivable}

[Princípio 1: perceptível - As informações e os componentes da interface do usuário têm de ser apresentados aos usuários de formas perceptíveis.](https://www.w3.org/TR/WCAG20/#perceivable)

### Alternativas em texto (1.1)      {#text-alternatives}

[Diretriz 1.1 Alternativas em texto: fornecer alternativas em texto para qualquer conteúdo não textual, para que seja possível alterá-lo para outras formas mais adequadas à necessidade do indivíduo, como impressão em caracteres ampliados, braille, fala, símbolos ou linguagem mais simples.](https://www.w3.org/TR/WCAG20/#text-equiv)

### Conteúdo não textual (1.1.1)      {#non-text-content}

* Critério de Sucesso 1.1.1
* Nível A
* Conteúdo não textual: todo o conteúdo não textual que é apresentado ao usuário tem uma alternativa em texto que serve um propósito equivalente, exceto para as situações indicadas abaixo.

#### Finalidade - Conteúdo não textual (1.1.1) {#purpose-non-text-content}

As informações em uma página da Web podem ser fornecidas em vários formatos não textuais diferentes, como imagens, vídeos, animações, gráficos e tabelas. Os indivíduos cegos ou com deficiências visuais graves não conseguem visualizar o conteúdo não textual, mas podem acessar o conteúdo textual através da leitura por um leitor de tela ou apresentado na forma tátil por um dispositivo de exibição em Braille. Portanto, ao disponibilizar alternativas em texto para o conteúdo no formato gráfico, os indivíduos que não conseguem visualizá-lo podem acessar uma versão equivalente das informações disponibilizadas.

Um benefício adicional útil é que as alternativas em texto permitem que o conteúdo não textual seja indexado pela tecnologia do mecanismo de pesquisa.

#### Como cumprir - Conteúdo não textual (1.1.1)      {#how-to-meet-non-text-content}

Para gráficos estáticos, o requisito básico é o de proporcionar uma alternativa em texto equivalente para o gráfico. Isso pode ser realizado no campo **Texto alternativo**:

>[!NOTE]
>
>Alguns componentes prontos para uso, como o **Carrossel** e a **Apresentação de slides**, não fornecem um meio de adicionar descrições de texto alternativas a imagens. Ao implementar as versões desses componentes para a instância do AEM, sua equipe de desenvolvimento precisará configurá-los para suportar o atributo `alt`[, para que os autores possam adicioná-lo ao conteúdo (consulte Adicionar suporte para elementos HTML e atributos adicionais](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

O campo **Texto alternativo** está disponível na guia propriedades **Avançadas** de imagem na caixa de diálogo do componente de ** Imagem:**

![Editar a caixa de diálogo do componente de Imagem na interface clássica; mostra o campo de Texto alternativo.](assets/chlimage_1-17a.png)

O AEM adiciona um **Texto alternativo** em suas imagens por padrão. Para a interface clássica existem dois cenários diferentes para a forma como o atributo padrão é criado (embora o valor padrão possa não ser suficiente como uma alternativa e provavelmente precisará ser editado na guia de propriedades ** Avançadas** de imagem):

* Arquivo:

   Uma imagem é carregada do disco rígido do usuário. If you add an image component to a page and then choose an image from your hard drive, or another source, the default value for **Alt Text** is `file`. Isso deve ser alterado na guia de propriedades **Avançadas** de imagem. Mais uma vez, esse valor não é exibido no campo **Texto alternativo,** mas quando é alterado, o novo valor é mostrado no campo.

* Ativo:

   Uma imagem é adicionada do repositório de ativos digitais. Se você arrastar uma imagem do repositório de ativos digitais para uma página da Web, em seguida, os valores **Título** e **Texto alternativo** serão transferidos dos metadados para a imagem.

>[!NOTE]
>
>In both of the above scenarios, the default **Alt Text** value is not visible in the **Advanced Image Properties** tab. To change the default value, simply enter a new value in the **Alt Text** field.

>[!NOTE]
>
>Se a imagem for meramente decorativa (consulte [Criar boas alternativas em texto](#creating-good-text-alternatives)), você pode inserir um espaço no campo **Texto alternativo** usando a barra de espaço. This will create an empty `alt` attribute, which will prompt a screen reader to ignore the image.

#### Criar boas alternativas de texto {#creating-good-text-alternatives}

Existem várias formas de conteúdo não textual, de modo que o valor da alternativa em texto dependerá da função que o gráfico vai desempenhar na página da Web. Algumas regras gerais que devem ser seguidas incluem:

* As alternativas em texto devem ser breves, mas devem capturar claramente as informações essenciais fornecidas pelo conteúdo não textual.
* Descrições excessivamente longas (mais de 100 caracteres) devem ser evitadas. Se um texto alternativo exigir mais detalhes:

   * forneça uma breve descrição no texto alternativo
   * e tiver uma descrição mais longa no texto em outro lugar na mesma página ou em uma página separada. Vincule para essa descrição separada, tornando a imagem um link ou colocando um link de texto adjacente à imagem.

* O texto alternativo não deve replicar o conteúdo fornecido no formulário de texto próximo à mesma página. Lembre-se que muitas imagens são ilustrações de pontos já abordados no texto de uma página, então é possível que já exista uma alternativa detalhada em texto.
* Se o conteúdo não textual for um link para outra página ou documento e não houver nenhum outro texto que faça parte do mesmo link, então o texto alternativo da imagem deve indicar o destino do link e não descrever a imagem.
* Se o conteúdo não textual estiver em um elemento de botão e não houver nenhum texto que faça parte do mesmo botão, então o texto alternativo da imagem deve indicar a funcionalidade do botão e não descrever a imagem.
* É perfeitamente aceitável disponibilizar para uma imagem um texto alternativo vazio (null), mas apenas se ela não tiver um texto alternativo (por exemplo, ela é um gráfico meramente decorativo) ou se o texto equivalente já existir no texto da página.

O [rascunho W3C: as técnicas de HTML5 para fornecer alternativas em texto úteis](https://dev.w3.org/html5/alt-techniques/) têm mais detalhes e exemplos da disposição adequada do texto alternativo para as imagens de tipos diferentes.

Tipos específicos de conteúdo não textual que necessitam de alternativas em texto podem incluir:

* Fotos ilustrativas:

   Estas são imagens de pessoas, objetos ou lugares. Think about the role of the photo in the page; an appropriate text equivalent is likely to be *Photo of[object ]*, but may be dependent on the surrounding text.

* Ícones:

   Estes são pequenos pictogramas (gráficos) que transmitem informações específicas. Eles devem ser usados de forma consistente em uma página e um site. Todas as instâncias do ícone em uma página ou um site devem ter a mesma alternativa em texto curta e sucinta, a menos que isso resulte em duplicação desnecessária do texto adjacente.

* Gráficos e gráficos:

   Normalmente, representam dados numéricos. Dessa forma, uma opção para fornecer uma alternativa em texto pode ser incluir um breve resumo das principais tendências indicadas na tabela ou gráfico. If necessary, also provide a more detailed description in text using the **Description** field in the **Advanced** image properties tab. Além disso, você pode fornecer os dados de origem em forma de tabela em outro lugar na página ou no site.

   ![Exemplo de um gráfico. Abaixo é apresentada a melhor abordagem para fornecer uma alternativa.](assets/chlimage_1-2a.jpeg)

   To provide an alternative for this example chart, add a concise `alt` text to the image itself and then follow the image with a full text alternative.

   ```xml
   <p><img src="figure1.gif" alt="Figure 1" ></p>
   <p> Figure 1. Distribution of Articles by Journal Category.
   Pie chart: Language=68%, Education=14% and Science=18%.</p>
   ```

   >[!NOTE]
   >
   >O trecho acima é usado apenas para ilustrar a ordem. Recomenda-se usar o componente de **Imagem** (em vez da referência `img src` usada acima).

   No AEM isso pode ser realizado usando uma combinação dos campos **Alternar texto** e **Descrição** na caixa de diálogo de configuração da imagem - conforme encontrado na seção [Como cumprir - Conteúdo sem texto (1.1.1)](#how-to-meet-non-text-content).

* Mapas, diagramas, fluxogramas:

   Para gráficos que fornecem dados espaciais (por exemplo, para ser compatível com a descrição das relações entre objetos ou um processo), verifique se a mensagem principal é fornecida no formato de texto.  Em mapas, fornecer um equivalente de texto completo provavelmente não será prático, mas se o mapa for fornecido como uma forma de ajudar as pessoas a encontrar o caminho para um determinado local, o texto alternativo da imagem do mapa poderá indicar brevemente o *Mapa de X* e, em seguida, fornecer direções para esse local no texto em outro lugar na página ou por meio do campo **Descrição** na guia **Avançado** do componente **Imagem**.

* CAPTCHAs:

   Um CAPTCHA é um *teste de Turing público completamente automatizado para diferenciação entre computadores e humanos*. É uma verificação de segurança usada em páginas da Web para diferenciar os humanos de um software mal-intencionado, mas que pode causar barreiras de acessibilidade. São imagens que exigem que os usuários descrevam o que visualizam, a fim de passar por um teste de segurança. Fornecer uma alternativa em texto para a imagem, obviamente, não é possível, portanto, em vez disso, você terá de considerar as soluções alternativas não gráficas.

   O W3C fornece uma série de sugestões, como: cada uma dessas abordagens tem suas próprias vantagens e desvantagens.

   * Enigmas de lógica
   * O uso da saída de som, em vez de imagens
   * Contas e filtros de spam de uso limitado.

* Imagens de plano de fundo:

   Isso é feito usando folhas de estilos em cascata (CSS) em vez de HTML. Isso significa que não é possível especificar um valor de texto alternativo. Por conseguinte, as imagens de fundo não devem fornecer informações textuais importantes - se o fizerem, essas informações também devem ser fornecidas no texto da página.

   No entanto, é importante que um plano de fundo alternativo seja mostrado quando a imagem não puder ser exibida.

   >[!NOTE]
   >
   >Deve haver um nível adequado de contraste entre o plano de fundo e o texto de primeiro plano; isso é abordado com mais detalhes na seção [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Mais informações - Conteúdo não contextual (1.1.1)      {#more-information-non-text-content}

* [Noções sobre o Critério de sucesso 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [Como cumprir o Critério de sucesso 1.1.1](https://www.w3.org/WAI/WCAG20/quickref/#text-equiv)
* [W3C: técnicas de HTML5 para fornecer alternativas em texto úteis (rascunho)](https://dev.w3.org/html5/alt-techniques/)
* [Explicação do W3C sobre as alternativas para CAPTCHAs](https://www.w3.org/TR/turingtest/)

### Mídia com base no tempo (1.2)      {#time-based-media}

[Diretriz de mídia com base no tempo 1.2: fornece alternativas para a mídia com base no tempo.](https://www.w3.org/TR/WCAG20/#text-equiv)

Trata-se de um conteúdo da Web que é *baseado no tempo*. Abrange o conteúdo que o usuário pode reproduzir (como vídeo, áudio e conteúdo animado) e pode ser pré-gravado ou ter transmissão ao vivo.

### Apenas áudio e apenas vídeo (pré-gravado) (1.2.1)    {#audio-only-and-video-only-pre-recorded}

* Critério de sucesso 1.2.1
* Nível A
* Apenas áudio e apenas vídeo (pré-gravado): para mídia somente de áudio e somente de vídeo pré-gravada, as informações a seguir são verdadeiras, exceto quando o áudio ou vídeo for uma alternativa em mídia para o texto e claramente identificada como tal:

   * Apenas áudio pré-gravado: uma alternativa para a mídia com base no tempo é fornecida, que apresenta informações equivalentes para o conteúdo composto apenas de áudio pré-gravado.
   * Apenas vídeo pré-gravado: é fornecida uma faixa de áudio ou uma alternativa para a mídia com base no tempo, que apresenta informações equivalentes para o conteúdo composto apenas de vídeo pré-gravado.

#### Propósito - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1)    {#purpose-audio-only-and-video-only-pre-recorded}

Problemas de acessibilidade para vídeo e áudio podem ser enfrentados por:

* Pessoas com deficiência visual, quando não há trilha sonora ou a mesma não é suficiente para informá-los sobre o que está acontecendo no vídeo ou animação;
* Pessoas com deficiências auditivas ou surdas, que não podem ouvir a trilha sonora;
* Pessoas que podem ouvir a trilha sonora, mas não entendem o que está sendo falado (por exemplo, porque está em um idioma que não entendem).

O vídeo ou áudio também pode estar disponível para as pessoas que utilizam navegadores ou dispositivos que não suportam a reprodução de conteúdo em formatos de mídia específicos, como o Adobe Flash.

Fornecer essas informações em um formato diferente, como texto (ou áudio para vídeo sem áudio), pode torná-lo acessível às pessoas que não conseguem acessar o conteúdo original.

#### Como cumprir - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1)    {#how-to-meet-audio-only-and-video-only-pre-recorded}

* Se o conteúdo for um áudio pré-gravado sem vídeo (como um podcast):

   * Forneça um link imediatamente antes ou depois do conteúdo para obter uma transcrição do texto do conteúdo de áudio.

      A transcrição deve ser uma página HTML com um equivalente em texto de todo o conteúdo falado e não-falado importante, além de uma indicação de quem está falando, uma descrição do cenário, expressões vocais e uma descrição de qualquer outro áudio significativo.

* Se o conteúdo for uma animação ou vídeo pré-gravado sem áudio:

   * Forneça um link imediatamente antes ou depois do conteúdo para uma descrição de texto equivalente das informações fornecidas pelo vídeo
   * Ou uma descrição de áudio equivalente em um formato de áudio normalmente utilizado, como MP3.

>[!NOTE]
>
>Se o conteúdo de áudio ou vídeo for disponibilizado como uma alternativa para o conteúdo que já existe em outro formato em uma página da Web, não há necessidade de seguir os requisitos acima. Por exemplo, se um vídeo exemplifica uma lista de instruções de texto, então não é necessário uma alternativa, já que essas instruções atuam como uma alternativa para o vídeo.

Inserir multimídia, especificamente um conteúdo em Flash, em suas páginas da Web do AEM é semelhante à inserção de uma imagem. No entanto, como o conteúdo multimídia é muito maior do que uma imagem estática, há diversas configurações e opções para controlar a forma como a multimídia é reproduzida.

>[!NOTE]
>
>Ao usar multimídia com um conteúdo informativo, é necessário criar também links para as alternativas. Por exemplo, para incluir uma transcrição de texto, crie uma página HTML para exibir a transcrição e, em seguida, adicione um link ao lado ou abaixo do conteúdo de áudio.

#### Mais informações - Apenas áudio e apenas vídeo (pré-gravado) (1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [Como cumprir o Critério de sucesso 1.2.1](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)

### Legendas (pré-gravadas) (1.2.2)    {#captions-pre-recorded}

* Critério de sucesso 1.2.2
* Nível A
* Legendas (pré-gravadas): as legendas são disponibilizadas para todo o conteúdo de áudio pré-gravado na multimídia sincronizada, exceto quando a mídia é uma alternativa para texto e é claramente identificada como tal.

#### Propósito - Legendas (pré-gravadas) (1.2.2)    {#purpose-captions-pre-recorded}

Os indivíduos surdos ou com deficiência auditiva não conseguirão ou terão grande dificuldade ao acessar o conteúdo de áudio. As legendas são equivalentes em texto para áudio falado e não falado, exibidas na tela no momento adequado durante o vídeo. Elas permitem que os indivíduos que não conseguem ouvir o áudio entendam o que está acontecendo.

>[!NOTE]
>
>As legendas não são necessárias onde o texto adequado ou os equivalentes não textuais (que fornecem informações diretamente equivalentes) estão disponíveis na mesma página que o vídeo ou a animação.

#### Como cumprir - Legendas (pré-gravadas) (1.2.2)    {#how-to-meet-captions-pre-recorded}

As legendas podem ser:

* Abertas: sempre visíveis quando o vídeo é reproduzido)
* Ocultas: as legendas podem ser ativadas ou desativadas pelo usuário

Use as legendas ocultas sempre que possível, já que proporcionam ao usuário a escolha de visualizar ou não as legendas. 

Para as legendas ocultas, será necessário criar e fornecer um arquivo de legenda sincronizada em um formato adequado (como [SMIL](https://www.w3.org/AudioVideo/)), junto com o arquivo de vídeo (os detalhes sobre como proceder estão fora do escopo desse guia, mas fornecemos links para alguns tutoriais em [Mais informações - Legendas (pré-gravadas) (1.2.2)](#more-information-captions-pre-recorded)). Certifique-se de fornecer uma nota para que os usuários saibam que as legendas estão disponíveis para o vídeo.

Se você precisar usar as legendas abertas, insira o texto na faixa de vídeo. Essa ação pode ser realizada utilizando aplicativos de edição de vídeo que permitem a sobreposição de títulos no vídeo.

#### Mais informações - Legendas (pré-gravadas) (1.2.2)    {#more-information-captions-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html):
* [Como cumprir o Critério de sucesso 1.2.2](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)
* [W3C: Multimídia sincronizada](https://www.w3.org/AudioVideo/)
* [Legendas, transcrições e descrições de áudio - pelo WebAIM](https://webaim.org/techniques/captions/)

### Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3)    {#audio-description-or-media-alternative-pre-recorded}

* Critério de Sucesso 1.2.3
* Nível A
* Descrição de áudio ou alternativa de mídia (pré-gravada): é fornecida uma descrição de áudio ou uma alternativa para mídia com base no tempo do conteúdo de vídeo pré-gravado para a mídia sincronizada, exceto quando a mídia for uma alternativa para texto e claramente identificada como tal. 

#### Propósito - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3)    {#purpose-audio-description-or-media-alternative-pre-recorded}

Os indivíduos que são cegos ou deficientes visuais vão enfrentar barreiras de acessibilidade se as informações em um vídeo ou uma animação forem fornecidas apenas visualmente, ou se a trilha sonora não fornecer informações suficientes para permitir a compreensão do que está acontecendo visualmente.

#### Como cumprir - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3)    {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

Existem duas abordagens que podem ser adotadas para atender a esse critério de sucesso. Ambas são aceitáveis:

1. Incluir uma descrição de áudio adicional para o conteúdo do vídeo. Isso pode ser feito de uma das três maneiras:

   * Durante as pausas no diálogo existente, forneça informações sobre as mudanças na cena que não são apresentadas como parte da faixa de áudio atual;
   * Forneça uma faixa de áudio nova, adicional e opcional contendo a trilha sonora original, mas incluindo também informações de áudio extras sobre as mudanças no cenário.

      * Isso permite que os usuários alternem entre a faixa de áudio existente (que *não* contém uma descrição de áudio) e a nova faixa de áudio (que *contém* uma descrição de áudio).
      * Isso evita a interrupção para os usuários que não precisam de descrição adicional.
   * Crie uma segunda versão do conteúdo de vídeo para permitir descrições de áudio estendidas. Isso reduz as dificuldades associadas à disponibilização de descrições de áudio detalhadas em lacunas entre o diálogo existente, pausando temporariamente o áudio e o vídeo em pontos adequados. Como resultado, uma descrição de áudio muito maior pode ser disponibilizada, antes que a ação inicie novamente. Como no exemplo anterior, essa é a melhor opção fornecida como uma faixa de áudio extra opcional, a fim de evitar a interrupção para os usuários que não precisam de uma descrição adicional.


1. Fornecer uma transcrição de texto que seja um equivalente de texto adequado dos elementos visuais e de áudio do vídeo ou animação. Isso deve incluir, conforme o caso, uma indicação de quem está falando, uma descrição da configuração e expressões vocais. Dependendo da extensão, você pode colocar a transcrição na mesma página que o vídeo ou a animação, ou em uma página separada; caso escolha a última opção, forneça um link para a transcrição ao lado do vídeo ou da animação.

Detalhes exatos de como criar um vídeo descrito por áudio estão fora do escopo desse guia. A criação de descrições de vídeo e áudio pode ser demorada, mas outros produtos da Adobe podem ajudar a realizar essas tarefas. Se você criar o conteúdo no Adobe Flash Professional, também será necessário criar um script para solicitar que o usuário baixe o plug-in adequado e fornecer uma alternativa em texto por meio do elemento `<noscript>`.

#### Mais informações - Descrição de áudio ou alternativa de mídia (pré-gravada) (1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html):
* [Como cumprir o Critério de sucesso 1.2.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://helpx.adobe.com/br/premiere-pro/using/whats-new.html)

### Legendas (ao vivo) (1.2.4)        {#captions-live}

* Critério de sucesso 1.2.4
* Nível AA
* Legendas (ao vivo): são fornecidas legendas para todo o conteúdo de áudio ao vivo na mídia sincronizada.

#### Propósito - Legendas (ao vivo) (1.2.4)      {#purpose-captions-live}

Esse critério de sucesso é idêntico às [Legendas (pré-gravadas)](#captions-pre-recorded), já que aborda as barreiras de acessibilidade enfrentadas pelos indivíduos surdos ou com deficiências auditivas, exceto que esse critério de sucesso lida com as apresentações ao vivo, como webcasts.

#### Como cumprir - Legendas (ao vivo) (1.2.4) {#how-to-meet-captions-live}

Siga as orientações fornecidas para as [Legendas (pré-gravadas)](#captions-pre-recorded) acima. No entanto, como a mídia é ao vivo, a disposição da legenda tem de ser criada o mais rapidamente possível e em resposta ao que está acontecendo. Portanto, você deve considerar o uso de legendagem em tempo real ou ferramentas de voz para texto.

Instruções detalhadas estão além do escopo desse documento, mas os seguintes recursos disponibilizam informações úteis:

* [WebAIM: legendagem em tempo real](https://www.webaim.org/techniques/captions/realtime.php)
* [AccessIT (University of Washington): as legendas podem ser geradas automaticamente usando reconhecimento de voz?](https://www.washington.edu/accessit/articles?1209)

#### Mais informações - Legendas (ao vivo) (1.2.4)    {#more-information-captions-live}

* [Noções sobre o Critério de sucesso 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [Como cumprir o Critério de sucesso 1.2.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-real-time-captions)

### Descrição de áudio (pré-gravado) (1.2.5)        {#audio-description-pre-recorded}

* Critério de Sucesso 1.2.5
* Nível AA
* Descrição de áudio (pré-gravado): é fornecida uma descrição de áudio para todos os conteúdos de vídeo pré-gravados em uma mídia sincronizada.

#### Propósito - Descrição de áudio (pré-gravado) (1.2.5)    {#purpose-audio-description-pre-recorded}

Esse critério de sucesso é idêntico à [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-pre-recorded), exceto que os autores devem fornecer uma descrição de áudio muito mais detalhada para estar em conformidade com o Nível AA.

#### Como cumprir - Descrição de áudio (pré-gravado) (1.2.5)    {#how-to-meet-audio-description-pre-recorded}

Siga as orientações fornecidas para a [Descrição de áudio ou alternativa de mídia (pré-gravada)](#audio-description-or-media-alternative-pre-recorded).

#### Mais informações - Descrição de áudio (pré-gravado) (1.2.5)    {#more-information-audio-description-pre-recorded}

* [Noções sobre o Critério de sucesso 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [Como cumprir o Critério de sucesso 1.2.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc-only)

### Adaptável (1.3)      {#adaptable}

[Diretriz adaptável 1.3: criar conteúdos que possam ser apresentados de diferentes formas (por exemplo, um layout mais simples) sem perder as informações ou a estrutura.](https://www.w3.org/TR/WCAG20/#content-structure-separation)

Essa diretriz abrange os requisitos necessários para auxiliar os indivíduos que:

* não conseguem acessar às informações apresentadas por um autor em um layout da página da Web *padrão *bidimensional, de várias colunas e colorido

* usam uma exibição visual alternativa ou apenas de áudio, como um texto grande ou contraste alto.

### Informações e Relações (1.3.1)          {#info-and-relationships}

* Critério de Sucesso 1.3.1
* Nível A
* Informações e Relações: as informações, a estrutura e as relações transmitidas através de apresentação podem ser determinadas de forma programática ou disponíveis no texto.

#### Propósito - Informações e Relações (1.3.1)      {#purpose-info-and-relationships}

Muitas tecnologias de assistência utilizadas por indivíduos com deficiência contam com informações estruturais, a fim de exibir ou produzir o conteúdo de forma eficiente. Essas informações estruturais podem assumir a forma de cabeçalhos de página, linha de tabela e cabeçalhos de coluna e tipos de lista. Por exemplo, um leitor de tela pode permitir que um usuário navegue por uma página de um cabeçalho a outro. No entanto, quando o conteúdo da página parece ter a estrutura somente por meio de um estilo visual, em vez do HTML subjacente, então não há informações estruturais disponíveis para as tecnologias de assistência, o que limita a sua capacidade para auxiliar a navegação mais fácil.

Esse critério de sucesso existe para garantir que a informação estrutural seja disponibilizada por meio de HTML, de modo que os navegadores e as tecnologias de assistência possam acessar e aproveitar as informações.

#### Como cumprir - Informações e Relações (1.3.1)     {#how-to-meet-info-and-relationships}

O AEM facilita a criação de páginas da Web usando os elementos de HTML adequados. Abra o conteúdo da página no RTE (um componente de Texto) e use o menu **Formatar** para especificar o elemento estrutural adequado (por exemplo, parágrafo, cabeçalho, etc.).

A imagem a seguir mostra o texto que foi estilizado como o texto do parágrafo; a exibição do código de origem usado mostra que ele tem as tags corretas de abertura e fechamento &lt;p> &lt;/p>.

![Um exemplo do elemento Parágrafo mostrado no modo de edição da origem (interface clássica).](assets/chlimage_1-18a.png)

É possível verificar se as suas páginas da Web têm a estrutura adequada através:

* **Utilização de cabeçalhos:**

   As long as you have the accessibility features of the RTE enabled (see [AEM and Accessibility](/help/sites-administering/rte-accessible-content.md)), AEM offers 3 levels of page heading. You can use these to identify sections and subsections of content. Heading 1 is the highest level of heading, Heading 3 the lowest. The system administrator can configure the system to allow the use of more heading levels.

   A imagem a seguir mostra um exemplo dos diferentes tipos de cabeçalhos.

   ![Os cabeçalhos H1 até o H3 são exibidos no seletor suspenso (interface clássica).](assets/chlimage_1-19a.png)

* **Texto destacado**:

   Use o elemento &lt;strong> ou&lt;em> para indicar ênfase. Não use os cabeçalhos para destacar o texto dentro dos parágrafos.

   * Destaque o texto que deseja enfatizar;
   * Click on the **B** icon (for &lt;strong>) or the **I** icon (for &lt;em>) shown within the **Properties** panel (make sure that HTML is selected).
   >[!NOTE]
   >
   >O RTE em uma instalação padrão do AEM está configurado para usar:
   >
   >* &lt;b> para &lt;strong>
   * &lt;i> para &lt;em>
   Eles são efetivamente iguais, mas &lt;strong> e &lt;em> são preferíveis, já que são um html semanticamente correto. Sua equipe de desenvolvimento pode configurar o RTE para usar &lt;strong> e &lt;em> (em vez de &lt;b> e &lt;i>), ao desenvolver a instância do projeto.

* **Use listas**: você pode usar o HTML para especificar três diferentes tipos de listas:

   * The `<ul>` element is used for *unordered* lists (bulleted) lists. Os itens da lista individual são identificados usando o elemento `<li>`.

      in the RTE, use the **Bulleted List** icon.

   * O elemento `<ol>` é usado para as listas *numeradas*. Os itens da lista individual são identificados usando o elemento `<li>`.

      No RTE, use o ícone **Lista numerada** .
   Caso deseje alterar o conteúdo existente em um tipo de lista específica, destaque o texto e selecione o tipo de lista adequado. Como no exemplo anterior que mostra como o texto do parágrafo é inserido, os elementos desejados da lista são adicionados automaticamente ao seu HTML, mas você pode visualizá-los na exibição da edição da fonte.

   >[!NOTE]
   `<dl>` não é suportado pelo RTE.

* **Use tabelas**:

   As tabelas de dados devem ser identificadas usando os elementos da tabela de HTML:

   * um elemento `<table>`
   * um elemento `<tr>` para cada linha da tabela
   * um elemento `<th>` para cada linha e cabeçalho da coluna
   * um elemento `<td>` para cada célula de dados
   >[!NOTE]
   As tabelas devem ser observadas com o componente **Tabela**. Embora as tabelas possam ser criadas no componente Texto, isso não é recomendado.

   Além disso, as tabelas acessíveis usam os seguintes elementos e atributos:

   * O elemento `<caption>` é usado para fornecer uma legenda visível para a tabela. As legendas por padrão são exibidas de forma centralizada acima da tabela, mas podem ser posicionadas adequadamente usando o CSS. A legenda é associada à tabela de forma programada, portanto, é um método útil para fornecer uma introdução ao conteúdo.
   * O elemento `<h3 class="summary">` auxilia os usuários com deficiências visuais a compreender de forma mais fácil as informações apresentadas em uma tabela, fornecendo um resumo do que pode ser visto. Isso é particularmente útil quando layouts complexos ou não convencionais são usados (esse atributo não é exibido no navegador, somente é lido nas tecnologias de assistência).
   * O `scope` atributo do elemento `<th>` é usado para indicar se uma célula representa um cabeçalho de uma linha ou de uma coluna específica. Uma abordagem semelhante é a de usar o cabeçalho e os atributos de id em tabelas complexas, onde as células de dados podem ser associadas a um ou mais cabeçalhos.
   >[!NOTE]
   Por padrão, esses elementos e atributos não estão diretamente disponíveis, embora o administrador do sistema possa adicionar o suporte para esses valores na caixa de diálogo **Propriedades da tabela**[ (consulte Adicionar suporte para outros elementos e atributos de HTML](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

   Ao adicionar uma **Tabela** é possível configurar as **Propriedades da tabela** usando uma caixa de diálogo.

   * Uma **Legenda** adequada.
   * Remova qualquer valor padrão para **Largura**, **Altura**, **Borda**, **Preenchimento da célula e** **Espaçamento entre células**. já que essas propriedades podem ser definidas em uma planilha de estilos global.
   ![Caixa de diálogo de propriedades da tabela.](assets/chlimage_1-20a.png)

   You can then use the **Cell properties** to choose whether the cell is a data or header cell and, if a header cell, whether it relates to a row or column or both:

   ![Caixa de diálogo das propriedades da célula; definir uma linha (geralmente a primeira) como a de cabeçalho.](assets/chlimage_1-21a.png)

* **Tabelas de dados complexos:**

   Em alguns casos, onde há tabelas complexas com dois ou mais níveis de cabeçalhos, as Propriedades da tabela básicas podem não ser suficientes para fornecer toda a informação estrutural necessária. Para esses tipos de tabelas complexas, relações diretas precisam ser criadas entre os cabeçalhos e as suas células relacionadas usando os atributos **cabeçalho** e **id**. Por exemplo, na tabela abaixo os cabeçalhos e IDs são combinados para fazer uma associação programática para usuários de tecnologia assistiva.

   >[!NOTE]
   O atributo id não está disponível em uma instalação predefinida. Ele pode ser ativado através da configuração de regras de HTML e do serializador no RTE.

   >[!NOTE]
   As tabelas devem ser observadas com o componente **Tabela**. Embora as tabelas possam ser criadas no componente Texto, isso não é recomendado.

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
   Essa funcionalidade não está disponível imediatamente em uma instalação padrão. Ela exige uma configuração de RTE; regras de HTML e serializador.

#### Mais informações - Informações e Relações (1.3.1) {#more-information-info-and-relationships}

* [Noções sobre o Critério de sucesso 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [Como cumprir o Critério de sucesso 1.3.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-programmatic)

### Características sensoriais (1.3.3)        {#sensory-characteristics}

* Critério de sucesso 1.3.3
* Nível A
* Características sensoriais: as instruções fornecidas para compreender e utilizar o conteúdo não dependem somente das características sensoriais dos componentes, como forma, tamanho, localização visual, orientação ou som.

#### Propósito - Características sensoriais (1.3.3)      {#purpose-sensory-characteristics}

Os designers muitas vezes se concentram nos recursos de design visual, como cor, forma, estilo de texto ou uma parte da posição absoluta ou relativa do conteúdo ao apresentar as informações. Esses recursos podem ser técnicas de design muito avançadas na transmissão de informações, mas os indivíduos cegos ou com deficiências visuais podem não conseguir acessar as informações que precisam da identificação visual dos atributos, como posição, cor ou forma.

Da mesma forma, as informações que exigem a distinção entre sons diferentes (por exemplo, o conteúdo falado masculino ou feminino) vão apresentar barreiras de acessibilidade para os indivíduos com deficiência auditiva, se não estiverem refletidas em nenhuma alternativa em texto para o conteúdo de áudio.

>[!NOTE]
Para os requisitos relacionados às alternativas de cor, consulte [Uso de cor](#use-of-color).

#### Como cumprir - Características sensoriais (1.3.3)      {#how-to-meet-sensory-characteristics}

Certifique-se de que todas as informações baseadas em características visuais do conteúdo da página também são apresentadas em um formato alternativo.

* Não se baseie na posição visual para fornecer informações. Por exemplo, se você deseja fazer uma referência para os usuários sobre um menu no lado direito da página para obter acesso a mais informações, não se refira ao *menu à direita*; em vez disso, nomeie o menu (por exemplo, através de um cabeçalho) e faça uma referência a esse nome no texto. 
* Não se baseie no estilo do texto (por exemplo, negrito ou itálico) como a única maneira de transmitir as informações.

>[!NOTE]
A utilização dos termos descritivos será aceitável se estes forem entendidos como relevantes em um contexto não visual. Por exemplo, normalmente é aceitável o uso dos termos *acima* e *abaixo,* já que sugerem, respectivamente, um conteúdo antes e depois de um item específico; isso ainda faria sentido com o conteúdo falado em voz alta.

#### Mais informações - Características sensoriais (1.3.3)      {#more-information-sensory-characteristics}

* [Noções sobre o Critério de sucesso 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [Como cumprir o Critério de sucesso 1.3.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-understanding)

### Discernível (1.4)      {#distinguishable}

[Diretriz 1.4 Discernível: facilitar a visualização e a audição de conteúdos aos usuários, incluindo a separação do primeiro plano e do plano de fundo. ](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### Utilização de cor (1.4.1)            {#use-of-color}

* Critério de Sucesso 1.4.1
* Nível A
* Utilização de cor: a cor não é utilizada como o único meio visual de transmitir informações, indicar uma ação, solicitar uma resposta ou distinguir um elemento visual.

>[!NOTE]
Esse critério de sucesso aborda especificamente a percepção da cor. Outras formas de percepção são abordadas na seção [Adaptável (1.3)](#adaptable); incluindo o acesso programático à cor e outras codificações de apresentação visual.

#### Propósito - Utilização de cor (1.4.1)      {#purpose-use-of-color}

A cor é, obviamente, uma forma eficaz de melhorar o apelo estético das páginas da Web e também é útil na transmissão de informações. No entanto, há uma série de deficiências visuais, da cegueira ao daltonismo, o que significa que algumas pessoas não conseguem distinguir entre certas cores. disponibilizar informações. 

Por exemplo, um indivíduo com daltonismo não conseguirá distinguir entre tons de verde e vermelho. É possível que ele veja as cores como uma terceira cor (por exemplo, marrom), nesse caso, o indivíduo não conseguirá distinguir entre o vermelho, verde e marrom.

Além disso, a cor pode não ser percebida por indivíduos que usam navegadores somente de texto, dispositivos com visor monocromático ou que exibem uma impressão em preto e branco da página.

#### Como cumprir - Utilização de cor (1.4.1)     {#how-to-meet-use-of-color}

Sempre que a cor for usada para transmitir informações, certifique-se de que a informação está disponível, sem a necessidade da visualização das cores.

Por exemplo, verifique se as informações fornecidas através das cores também estão evidentes no texto. A ilustração abaixo mostra como a cor e o texto indicam a disponibilidade de assentos para um show:

<table>
 <tbody>
  <tr>
   <td><p><strong>Show</strong></p> </td>
   <td><p><strong>Disponibilidade</strong></p> </td>
  </tr>
  <tr>
   <td><p>Terça-feira, 16 de março<sup></sup></p> </td>
   <td><p>ASSENTOS DISPONÍVEIS</p> </td>
  </tr>
  <tr>
   <td><p>Quarta-feira, 17 de março</p> </td>
   <td><p>ASSENTOS DISPONÍVEIS</p> </td>
  </tr>
  <tr>
   <td><p>Quinta-feira, 18 de março<sup></sup></p> </td>
   <td><p>ESGOTADO</p> </td>
  </tr>
 </tbody>
</table>

Se a cor for usada como dica para fornecer informações, você deve fornecer uma dica visual adicional, como a alteração do estilo (por exemplo, negrito, itálico) ou da fonte. Isso ajuda as pessoas com pouca visão ou daltonismo a identificar as informações. No entanto, não é possível depender dessas opções completamente, uma vez que isso não ajudará os indivíduos que não conseguem visualizar nada na página.

#### Mais informações - Utilização de cor (1.4.1) {#more-information-use-of-color}

* [Noções sobre o Critério de sucesso 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Como cumprir o Critério de sucesso 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Orientação sobre como atender a uma relação de contraste de 3:1, com uma lista de cores “seguras para usar na Web”](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### Contraste (Mínimo) (1.4.3)    {#contrast-minimum}

* Critério de Sucesso 1.4.3
* Nível AA
* Contraste (Mínimo): a apresentação visual e as imagens do texto têm uma relação de contraste de, no mínimo, 4.5:1, exceto para o seguinte:

   * Texto ampliado: o texto ampliado e as imagens compostas por texto ampliado têm uma relação de contraste de, no mínimo, 3:1.
   * Incidental: o texto ou as imagens de texto que fazem parte de um componente de interface de usuário inativo, que são meramente decorativos, e não estão visíveis para ninguém ou que são parte de uma imagem que inclui outro conteúdo visual significativo, não têm requisito de contraste.
   * Logotipos: o texto que faz parte de um logotipo ou marca comercial não tem requisito de contraste.

#### Propósito - Contraste (Mínimo) (1.4.3)     {#purpose-contrast-minimum}

Os indivíduos com certas deficiências visuais podem não conseguir distinguir entre determinados pares de cores com baixo contraste. Problemas de acessibilidade podem ocorrer para esses indivíduos, se:

*  O texto contrasta mal com a cor de fundo.
* A codificação de cores do texto (como o texto do link e texto comum) for importante para diferenciar as informações.

>[!NOTE]
O texto usado exclusivamente para fins decorativos está excluído desse critério de sucesso.

#### Como cumprir - Contraste (Mínimo) (1.4.3)      {#how-to-meet-contrast-minimum}

Verifique se o texto contrasta o suficiente com o plano de fundo. As relações de contraste dependem do tamanho e do estilo do texto em questão:

* Para texto com menos de 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste entre o texto/imagens de texto e o plano de fundo deve ser, pelo menos, 4.5:1.
* Para o texto com até 18 pontos (ou 14 pontos em negrito) em tamanho, a relação de contraste deve ser de pelo menos 3:1.
* Se um plano de fundo for estampado, então ele deve ser sombreado ao redor do texto, de modo que a relação 4.5:1 ou 3:1 seja mantida.

Para verificar as relações de contraste, use uma ferramenta de contraste em cores, como o [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) ou o [verificador de contraste em cores do WebAIM](https://www.webaim.org/resources/contrastchecker/). Essas ferramentas permitem que você verifique os pares de cores e informe quaisquer problemas de contraste.

De forma alternativa, se você estiver menos preocupado sobre como especificar a aparência de sua página, é possível optar por não especificar as cores do texto de plano de fundo e de primeiro plano. Nenhuma verificação de contraste é necessária, já que o navegador do usuário determinará as cores do texto e plano de fundo.

Se não for possível atender aos níveis de contraste recomendados, será necessário fornecer um link para uma versão alternativa equivalente da página (que não tenha problemas de contraste de cor), ou permitir que o usuário ajuste o contraste do esquema de cores da página de acordo com as suas próprias necessidades.

#### Mais informações - Contraste (Mínimo) (1.4.3)      {#more-information-contrast-minimum}

* [Noções sobre o Critério de sucesso 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [Como cumprir o Critério de sucesso 1.4.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-contrast)

### Imagens de texto (1.4.5)    {#images-of-text}

* Critério de Sucesso 1.4.5
* Nível AA
* Imagens de texto: se as tecnologias usadas puderem obter a apresentação visual, o texto será usado para transmitir as informações, em vez das imagens de texto, exceto para o seguinte:

   * Personalizável: a imagem do texto pode ser visualmente personalizada para as necessidades do usuário;
   * Básico: uma apresentação específica do texto é fundamental para a transmissão das informações.

>[!NOTE]
Os logotipos (texto que faz parte de um logotipo ou marca comercial) são considerados fundamentais.

#### Propósito - Imagens de texto (1.4.5)      {#purpose-images-of-text}

As imagens de texto são usadas, frequentemente, quando um estilo de texto específico é o preferido; por exemplo, um logotipo ou se o texto foi gerado de uma outra fonte (por exemplo, uma verificação de um documento em papel). No entanto, em comparação com o texto apresentado em HTML e o estilo usando CSS, as imagens de texto não têm flexibilidade para mudar o tamanho ou aparência, o que pode ser necessário para os indivíduos com deficiência visual ou dificuldade de leitura.

#### Como cumprir - Imagens de texto (1.4.5)      {#how-to-meet-images-of-text}

Se as imagens de texto tiverem que ser utilizadas, use o CSS para substituir as imagens de texto pelo texto equivalente em HTML, para que o texto seja disponibilizado de forma personalizada. Para ver um exemplo, consulte o [C30: usar o CSS para substituir o texto por imagens de texto e fornecer controles de interface do usuário para fazer a alteração](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Mais informações - Imagens de texto (1.4.5)      {#more-information-images-of-text}

* [Noções sobre o Critério de sucesso 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [Como cumprir o Critério de sucesso 1.4.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-text-presentation)

## Princípio 2: operável      {#principle-operable}

[Princípio 2: operável - os componentes da interface de usuário e a navegação precisam ser operáveis.](https://www.w3.org/TR/WCAG20/#operable)

### Pausar, Interromper, Ocultar (2.2.2)        {#pause-stop-hide}

* Critério de Sucesso 2.2.2
* Nível A
* Pausar, Interromper, Ocultar: para mover, piscar, deslocar ou atualizar automaticamente as informações, as seguintes opções são verdadeiras:

   * Mover, piscar, deslocar: para qualquer movimento, modo intermitente ou deslocamento, que (a) é iniciado automaticamente, (b) dura mais de cinco segundos e (c) seja apresentado em paralelo com outro conteúdo, existe um mecanismo para o usuário pausar, interromper ou ocultar, a menos que o movimento, o modo intermitente ou o deslocamento seja parte fundamental de uma atividade;
   * Atualizar automaticamente: para atualizar automaticamente qualquer informação que (a) é iniciada automaticamente e (b) seja apresentada em paralelo com outro conteúdo, existe um mecanismo para o usuário pausar, interromper ou ocultar, ou para controlar a frequência da atualização, a menos que a opção para atualizar automaticamente seja parte fundamental de uma atividade.

Os pontos para observar são:

1. Para os requisitos relacionados ao conteúdo no modo intermitente ou piscante, consulte [Não criar o conteúdo em uma forma conhecida por causar convulsões (2.3)](#seizures).
1. Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário em utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte o [Requisito de conformidade 5: não interferência](https://www.w3.org/TR/WCAG20/#cc5).
1. O conteúdo que é atualizado periodicamente pelo software ou que é transmitido para o agente de usuário, não é obrigado a preservar ou apresentar as informações geradas ou recebidas entre o início da pausa e a retomada da apresentação, pois isso pode não ser tecnicamente possível e, em muitas situações, pode induzir ao erro. 
1. Uma animação que ocorre como parte de uma fase de pré-carregamento ou uma situação similar pode ser considerada essencial se a interação não puder ocorrer durante essa fase para todos os usuários, e se não indicar o progresso, poderá confundir os usuários ou levá-los a pensar que o conteúdo foi congelado ou interrompido.

#### Propósito - Pausar, Interromper, Ocultar (2.2.2)      {#purpose-pause-stop-hide}

Alguns usuários podem achar que o conteúdo que se move é perturbador e dificulta a concentração em outras partes da página. Além disso, esse conteúdo pode ser de difícil leitura para os indivíduos que têm problemas para acompanhar o texto em movimento.

#### Como cumprir - Pausar, Interromper, Ocultar (2.2.2)      {#how-to-meet-pause-stop-hide}

Dependendo da natureza do conteúdo, você pode aplicar uma ou mais das seguintes sugestões ao criar as páginas da Web com um conteúdo em movimento, em modo intermitente ou piscante:

* Forneça um meio de pausar o deslocamento do conteúdo para proporcionar aos usuários tempo suficiente para lê-lo. Por exemplo, painéis de notícias ou um texto atualizado automaticamente.
* Verifique se o conteúdo em modo intermitente é interrompido após cinco segundos.
* Use as tecnologias adequadas para exibir um conteúdo em modo intermitente que possa ser desativado pelo navegador. Por exemplo, os arquivos Graphics Interchange Format (GIF) ou Animated Portable Network Graphics (APNG).
* Forneça um controle de formulário na página da Web para permitir que o usuário desative todos os conteúdos em modo intermitente da página.
* Se nenhuma das situações anteriores for possível, forneça um link para uma página que contenha todo o conteúdo, mas sem o modo intermitente.

#### Mais informações - Pausar, Interromper, Ocultar (2.2.2)     {#more-information-pause-stop-hide}

* [Noções sobre o Critério de sucesso 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [Como cumprir o Critério de sucesso 2.2.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-time-limits-pause)

### Convulsões (2.3)    {#seizures}

[Diretriz Convulsões 2.3: não crie o conteúdo em uma forma conhecida por causar convulsões](https://www.w3.org/TR/WCAG20/#seizure)

### Três flashes ou abaixo do limite (2.3.1)    {#three-flashes-or-below-threshold}

* Critério de Sucesso 2.3.1
* Nível A
* Três flashes ou Abaixo do limite: as páginas da Web não incluem qualquer conteúdo com mais de três flashes no período de um segundo ou o flash encontra-se abaixo dos limites de flash universal e flash vermelho.

>[!NOTE]
Como qualquer conteúdo que não cumpre este critério de sucesso pode interferir na capacidade de um usuário em utilizar a página inteira, todo o conteúdo da página da Web (quer seja ou não utilizado para cumprir outros critérios de sucesso) tem de cumprir este critério. Consulte o [Requisito de conformidade 5: não interferência](https://www.w3.org/TR/WCAG20/#cc5).

#### Finalidade - Três flashes ou Abaixo do limite (2.3.1) {#purpose-three-flashes-or-below-threshold}

Em certos casos, os flashes podem causar convulsões fotossensíveis. Este critério de sucesso permite aos usuários acessar e utilizar todo o conteúdo sem se preocupar com o conteúdo com flashes.

#### Como cumprir - Três flashes ou Abaixo do limite (2.3.1)      {#how-to-meet-three-flashes-or-below-threshold}

É necessário adotar algumas medidas para se certificar de que as seguintes técnicas são aplicadas:

* Garantir que nenhum componente do conteúdo tenha mais de três flashes no período de um segundo;
* Se a condição acima não puder ser cumprida, exibir o conteúdo em modo flash em uma *área pequena de segurança* em pixels na tela. Essa área é calculada utilizando uma fórmula complexa, abordada em [G176: manter a área de flashes suficientemente pequena](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), de modo que essa técnica só deve ser seguida se o conteúdo em modo flash for *absolutamente* necessário.

#### Mais informações - Três flashes ou Abaixo do limite (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Noções sobre o Critério de sucesso 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [Como cumprir o Critério de sucesso 2.3.1](https://www.w3.org/WAI/WCAG20/quickref/#seizure)

### Página com título (2.4.2)        {#page-titled}

* Critério de sucesso 2.4.2
* Nível A
* Página com título: as páginas da Web têm títulos que descrevem o tópico ou a finalidade.

#### Finalidade - Página com título (2.4.2)      {#purpose-page-titled}

Este critério de sucesso ajuda as pessoas, independentemente de qualquer incapacidade cognitiva, a identificar o conteúdo de uma página da Web sem precisar ler toda a página. Isso é especialmente útil quando várias páginas da Web estão abertas em abas de navegador, já que o título da página é exibido na aba e, portanto, pode ser localizado rapidamente.

#### Como cumprir - Página com título (2.4.2)      {#how-to-meet-page-titled}

Quando uma nova página HTML é criada no AEM, é possível especificar o título da página. Verifique se o título descreve adequadamente o conteúdo da página, para que os visitantes possam identificar rapidamente se o conteúdo é realmente relevante para as suas necessidades.

You can also edit the page title when editing a page, which is accessible by **Sidekick** - **Page** tab - **Page Properties...**

#### Mais informações - Página com título (2.4.2) {#more-information-page-titled}

* [Noções sobre o Critério de sucesso 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [Como cumprir o Critério de sucesso 2.4.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-title)

### Finalidade do link (em contexto) (2.4.4)        {#link-purpose-in-context}

* Critério de sucesso 2.4.4
* Nível A
* Finalidade do link (em contexto): a finalidade de cada link pode ser determinada a partir apenas do texto do link ou a partir do texto do link juntamente com o respectivo contexto do link determinado de forma programática, exceto quando a finalidade do link for ambígua para os usuários em geral.

#### Finalidade - Finalidade do link (Em contexto) (2.4.4)      {#purpose-link-purpose-in-context}

Para todos os usuários, independentemente da incapacidade cognitiva, indicar claramente a direção de um link por meio de um texto de link adequado é fundamental. Isso ajuda os usuários a decidir se querem ou não seguir um link. Para usuários deficientes visuais, um texto de link significativo é extremamente útil quando há vários links em uma página (principalmente se a página incluir excesso de texto), já que textos de link significativos fornecem uma indicação mais clara da funcionalidade da página de destino. Os usuários de tecnologias assistivas, que podem gerar uma lista de todos os links de uma página, podem compreender com mais facilidade o texto do link fora de contexto.

#### Como cumprir - Finalidade do link (Em contexto) (2.4.4)     {#how-to-meet-link-purpose-in-context}

Acima de tudo, verifique se a finalidade de um link está claramente descrita no texto.

* Exemplo incorreto:

   * Texto: para obter mais informações sobre nossas aulas noturnas no segundo trimestre de 2010, clique aqui .
   * Motivo: não indica clara e inequivocamente o seu destino.

* Exemplo correto:

   * Texto: aulas à noite para o segundo trimestre de 2010 - mais informações.
   * Motivo: ao ajustar levemente o texto e a posição do elemento de link, o texto pode ser melhorado:

Os links devem ser redigidos de forma consistente ao longo das páginas, principalmente em barras de navegação. Por exemplo, se um link para uma página específica for chamado de **Publicações** em uma página, use esse termo nas outras páginas para garantir a consistência.

Contudo, ao escrever, há algumas questões que envolvem o uso de títulos:

* O texto do atributo título geralmente está disponível apenas para usuários de mouse como uma pop-up de dica de ferramenta e não pode ser acessado &#x200B;&#x200B;usando o teclado.
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
O snippet acima é uma ilustração; recomenda-se usar o componente **Imagem**.

Embora seja aconselhável fornecer um texto de link que identifique a finalidade do link sem a necessidade de contexto adicional, reconhece-se que isto nem sempre é possível. Link contextuais gratuitos podem ser usados nos casos a seguir, exemplos de HTML que podem ser encontrados em [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs).

* Sempre que o texto do link fizer parte de uma lista de links estritamente relacionados e quando um item de lista que delimita o link fornecer contexto suficiente.
* Sempre que a finalidade de um link puder ser claramente identificada no texto do parágrafo *anterior* (não o seguinte).
* Quando o link estiver contido em uma tabela de dados e, portanto, a finalidade puder ser claramente identificada nos cabeçalhos associados.
* Sempre que uma lista de links estiver contida em um conjunto de cabeçalhos e o próprio cabeçalho fornecer o contexto apropriado.
* Sempre que uma lista de links estiver contida em um link aninhado e o item de lista principal acima do link aninhado fornecer o contexto apropriado.

Em alguns casos, quando existirem vários links em uma página (cada um dos quais fornecendo a direção de um link em detalhes complexos, mas necessários), pode ser apropriado fornecer uma versão alternativa da página da Web que mostre exatamente o mesmo conteúdo, mas sem um texto de link tão detalhado.

Alternativamente, scripts podem ser usados &#x200B;&#x200B;de modo que uma quantidade mínima de texto seja fornecida no próprio link e, ao ativar um controle apropriado posicionado na parte superior da página, o texto do link seja *expandido* para fornecer mais detalhes. Uma abordagem semelhante é a utilização de CSS para *ocultar* o link completo para usuários deficientes visuais, mas ainda exibi-lo na íntegra para os usuários de leitores de tela. Isso está fora do âmbito deste documento, mas mais informações sobre a forma como conseguir isso podem ser encontradas na seção [Mais Informações - finalidade do Link (Em Contexto) (2.4.4)](#more-information-link-purpose-in-context).

#### Mais informações - Finalidade do link (no contexto) (2.4.4) {#more-information-link-purpose-in-context}

* [Noções sobre o Critério de sucesso 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [Como cumprir o Critério de sucesso 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs)
* [C7: utilizar CSS para ocultar uma parte do texto do link](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## Princípio 3: compreensível    {#principle-understandable}

[Princípio 3: compreensível - A informação e a operação da interface do usuário devem ser compreensíveis.](https://www.w3.org/TR/WCAG20/#understandable)

### Torne o conteúdo do texto legível e compreensível (3.1)      {#make-text-content-readable-and-understandable}

[Diretriz 3.1 Legível: tornar o conteúdo do texto legível e compreensível.](https://www.w3.org/TR/WCAG20/#meaning)

### Idioma da página (3.1.1)      {#language-of-page}

* Critério de Sucesso 3.1.1
* Nível A
* Idioma da página: o idioma humano predefinido de cada página da Web pode ser determinado de forma programática.

#### Finalidade - Idioma da página (3.1.1)      {#purpose-language-of-page}

A finalidade deste critério de sucesso é garantir que o texto e outro conteúdo linguístico sejam apresentados corretamente. Para leitores de tela, isso garante que o conteúdo seja pronunciado corretamente. Para navegadores visuais, aumenta a probabilidade de apresentar determinados conjuntos de caracteres definidos corretamente.

#### Como cumprir - Idioma da página (3.1.1)      {#how-to-meet-language-of-page}

Para cumprir este critério de sucesso, o idioma padrão de uma página da Web pode ser identificado usando o atributo `lang`dentro do elemento`<html>` no topo da página. Por exemplo:

* Se uma página for escrita em inglês britânico, o elemento `<html>` deverá informar:

   `<html lang = “en-gb”>`

* Para processar uma página como inglês dos EUA, deverá ser adotado o seguinte padrão:

   `<html lang = “en-us”>`

No AEM, o idioma padrão da sua página é definido ao criá-la, mas também pode ser alterado durante a edição de uma página, acessível em **Sidekick** - guia **Página** - **Propriedades da página...** - guia **Avançadas**.

#### Mais Informações - Idioma da Página (3.1.1) {#more-information-language-of-page}

* [Noções sobre o Critério de sucesso 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [Como cumprir o Critério de sucesso 3.1.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-doc-lang-id)
* Os códigos são baseados em ISO 639-1. Uma lista mais extensa de códigos para cada idioma pode ser encontrada no [site W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de Partes (3.1.2)            {#language-of-parts}

* Critério de Sucesso 3.1.2
* Nível AA
* Idioma de Partes: o idioma humano de cada passagem ou frase do conteúdo pode ser determinado de forma programática, exceto para os nomes próprios, termos técnicos, palavras de idioma indeterminado e palavras ou frases que se tornaram parte do vernáculo do texto imediatamente circundante.

#### Finalidade - Idioma de Partes (3.1.2)      {#purpose-language-of-parts}

A finalidade deste critério de sucesso é semelhante ao critério de sucesso de [Idioma da Página ](#language-of-page), exceto que se aplica a páginas da Web com conteúdo em múltiplos idiomas em uma única página (por exemplo, devido a citações ou palavras incomuns).

As páginas que aplicam este critério de sucesso:

* Permitem que o software de tradução em braille insira caracteres acentuados.
* Permitem que os leitores de tela pronunciem corretamente as palavras em idioma diferente do padrão.
* Permitem que as ferramentas de tradução, como o Google Translate, traduzam corretamente o conteúdo de um idioma para outro.

#### Como Cumprir - Idioma de Partes (3.1.2)      {#how-to-meet-language-of-parts}

O atributo `lang` pode ser utilizado para identificar alterações no idioma do conteúdo. Por exemplo, uma citação em alemão (ISO 639-1, código “de”) pode ser apresentada da seguinte maneira:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
Blocos de citação não são suportados em uma instância predefinida. Um componente personalizado pode ser desenvolvido para suportar o recurso.

Da mesma forma, o navegador poderá processar uma palavra incomum ou frase corretamente se o elemento `span` for usado da seguinte maneira:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</span>.</p>
```

>[!NOTE]
Não é necessário seguir este critério de sucesso ao incluir nomes ou cidades em diferentes idiomas, ou ao usar palavras de empréstimo ou frases que se tornaram comuns no idioma padrão (como *schadenfreude* em inglês).

Para adicionar o elemento span, com um idioma apropriado, você pode editar manualmente a sua marcação HTML no modo de edição de fonte da RTE para ser exibido como acima. Como alternativa, o atributo `lang`[ pode ser incluído na RTE pelo administrador do sistema (consulte Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

#### Mais Informações - Idioma de Partes (3.1.2) {#more-information-language-of-parts}

* [Noções sobre o Critério de sucesso 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html)
* [Como cumprir o Critério de sucesso 3.1.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-other-lang-id)

### Ajude os usuários a evitar e corrigir erros (3.3)    {#help-users-avoid-and-correct-mistakes}

[Diretriz 3.3 Assistência de entrada: ajudar os usuários a evitar e corrigir erros](https://www.w3.org/TR/WCAG20/#minimize-error)

### Etiquetas ou Instruções (3.3.2)    {#labels-or-instructions}

* Critério de Sucesso 3.3.2
* Nível A
* Etiquetas ou Instruções: as etiquetas ou instruções são fornecidas quando o conteúdo exigir a entrada do usuário.

#### Finalidade - Etiquetas ou Instruções (3.3.2)      {#purpose-labels-or-instructions}

Fornecer instruções para ajudar as pessoas a preencher formulários é uma parte fundamental das boas práticas de usabilidade da interface. Fazer isso é particularmente útil para pessoas com deficiências visuais ou cognitivas que de outra forma poderiam ter dificuldade para entender o layout de um formulário e o tipo de dados a ser fornecido em um campo de formulário específico.

No AEM, uma etiqueta padrão é adicionada quando você adiciona um componente de formulário, como um **Campo de Texto**, à página. Este título padrão é dependente do tipo de componente. Você pode adicionar seu próprio título na guia **Título e Texto** da janela de edição desse campo. É importante garantir que as etiquetas ajudem os usuários a compreender os dados associados a cada componente do formulário.

![Guia Título e Texto (janela de edição); o titulo &#39;Descrição&#39; foi adicionado.](assets/chlimage_1-22a.png)

Este campo de **Título** deve ser usado para elementos de campo, pois fornece uma etiqueta que está disponível para tecnologia assistiva. Apenas escrever uma etiqueta no texto ao lado do campo não é suficiente.

Para alguns componentes de formulário, também é possível ocultar as etiquetas visualmente usando a opção **Ocultar Título**. Marcadores ocultos ainda estão disponíveis para a tecnologia assistiva, mas não são exibidos na tela. Embora esta possa ser uma boa abordagem em algumas situações, geralmente é melhor incluir uma etiqueta visual sempre que possível, pois alguns usuários podem estar olhando para uma pequena seção da tela (um campo por vez) e precisam de etiquetas para identificar o campo corretamente.

#### Botões de imagem {#image-buttons}

Quando são utilizados botões de imagem (por exemplo, o componente **Botão de Imagem**), o campo **Título** na guia **Título e Texto** da janela de edição fornece o texto alternativo para a imagem, em vez da etiqueta. Assim, no exemplo abaixo, a imagem com o texto `Submit`tem o texto alternativo de `Submit`, adicionado usando o campo **Título** na janela de edição.

![Botão de imagem com o texto alternativo definido no campo Título (janela de edição).](assets/chlimage_1-23a.png)

#### Grupos de campos de formulário {#groups-of-form-fields}

Se houver um grupo de controles relacionados, como **Grupo de opções**, pode ser necessário um título para o grupo, bem como controles individuais. Ao adicionar um conjunto de botões de opção na AEM, o campo **Título** fornece o título do grupo, enquanto os títulos individuais especificados como botões de opção (**Itens**) são criados.

![Adicionando itens ao grupo de opções. O título do grupo é &#39;Entrar em contato por&#39; - definido no campo Título.](assets/chlimage_1-24a.png)

Contudo, não existe uma associação programática entre o título do grupo e os próprios botões de opção. Editores de modelo precisam envolver o título nas tags `fieldset` e `legend` necessárias para criar esta associação e isso só pode ser feito através da edição do código fonte da página. Alternativamente, um administrador do sistema pode adicionar suporte a esses elementos para que eles apareçam na janela **Propriedades do Campo**[ (Consulte Adicionar suporte para elementos e atributos HTML adicionais](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

#### Considerações adicionais para formulários {#additional-considerations-for-forms}

Se os dados devem ser inseridos em um formato específico, deixe isso claro no texto da etiqueta. Por exemplo, se uma data deve ser inscrita no formato `DD-MM-YYYY`, indique isso especificamente como parte da etiqueta. Isto significa que quando os usuários de leitores de tela encontrarem o campo, a etiqueta será anunciada automaticamente, juntamente com as informações adicionais sobre o formato.

Se a entrada de um campo de formulário for obrigatória, deixe isso claro usando a palavra &quot;obrigatório&quot; como parte do rótulo. O AEM adiciona um asterisco quando um campo é obrigatório, mas seria ideal incluir a palavra `required` na própria etiqueta (no campo **Título** na janela de edição).

![Adicione informações adicionais (a palavra “obrigatório”) para os usuários de leitores de tela no campo &#39;Título&#39;.](assets/chlimage_1-25a.png)

O posicionamento das etiquetas também é importante, pois ajuda a localizar os campos apropriados. Isto é de especial importância quando o usuário se depara com um formulário complexo. Siga a convenção abaixo:

* Caixas de seleção ou botões de opção:

   As etiquetas são posicionadas imediatamente à direita do campo.

* Todos os outros componentes do formulário (por exemplo, caixas de texto, caixas de combinação):

   As etiquetas são posicionadas imediatamente acima ou à esquerda do campo.

Em formulários simples, com funcionalidade muito limitada, a identificação adequada de um botão `Submit` pode servir como etiqueta para o campo adjacente (por exemplo, `Search`). Isso é útil em situações em que encontrar espaço para o texto da etiqueta pode ser difícil.

#### Mais Informações - Etiquetas ou Instruções (3.3.2)      {#more-information-labels-or-instructions}

* [Noções sobre o Critério de sucesso 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [Como cumprir o Critério de sucesso 3.3.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-minimize-error-cues)

