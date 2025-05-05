---
title: Práticas recomendadas para formulários HTML5
description: Ajuste seu HTML5 Forms baseado em XFA para obter o melhor desempenho.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Práticas recomendadas para formulários HTML5{#best-practices-for-html-forms}

## Visão geral {#overview}

O AEM Forms tem um componente chamado HTML5 forms. Ajuda a renderizar PDF forms (arquivos XDP) existentes baseados em XFA no formato HTML5. Este documento fornece diretrizes e recomendações para reduzir o tempo de carregamento e melhorar o desempenho dos formulários HTML5 em dispositivos móveis.

A maioria dos dispositivos móveis tem um poder de processamento e recursos de memória limitados. Isso ajuda a melhorar o tempo de espera dos dispositivos móveis. Os navegadores da Web em execução em um dispositivo móvel têm acesso a recursos limitados (memória e recursos de processamento limitados). Quando o limite é atingido, o comportamento do navegador fica lento. Este documento fornece recomendações para manter o tamanho de um formulário HTML5 sob controle. Uma forma menor não viola os limites de memória e poder de processamento de um dispositivo e fornece uma experiência suave.

Embora as recomendações discutidas neste artigo sejam direcionadas para formulários HTML5, elas são igualmente aplicáveis aos PDF forms baseados em XFA. Essas práticas recomendadas contribuem coletivamente para o desempenho geral dos formulários HTML5. Requer um planejamento cuidadoso para desenvolver formas eficientes e produtivas. Vamos começar:

## Os nós são a moeda de formulários HTML5, gastá-los sabiamente {#nodes-are-currency-of-html-forms-spend-them-wisely}

Geralmente, um formulário XFA tem vários elementos. Por exemplo, tabela, campo de texto e imagens. Cada elemento tem várias propriedades para controlar o comportamento e a aparência do elemento. Quando um formulário XFA é renderizado no formato HTML5, todos os elementos XFA e as propriedades correspondentes são convertidos em nós DOM de modelo ou HTML. Esses nós aumentam o tamanho e a complexidade de um DOM. Tornando o formulário HTML5 lento para renderização.

É mais fácil para os navegadores renderizarem um DOM mais enxuto. Assim, você pode executar as seguintes otimizações em um formulário XFA para reduzir o número de nós. Portanto, gere uma estrutura DOM enxuta:

* Use a propriedade caption para adicionar um rótulo a um campo. Não use um elemento Text separado para adicionar um rótulo. Ajuda a perder peso extra, levando a ganhos de desempenho. Também ajuda a evitar problemas de layout.
* Mantenha o número mínimo de elementos de texto Draw em um formulário. Os elementos do Draw são úteis para melhorar a legibilidade e a aparência, mas não têm recursos de armazenamento de informações. É recomendável mesclar vários elementos de texto do Draw em um único elemento de texto do Draw. Não deixe pedra sobre pedra para tornar uma forma mais enxuta.

## Os formulários Lite têm melhor desempenho, mantenha os recursos compactados {#lite-forms-perform-better-keep-the-resources-compressed}

Um formulário HTML5 pode conter vários recursos externos, como arquivos de imagem, JavaScript e CSS. Toda vez que um navegador solicita um formulário, os recursos externos são enviados pela rede. O tempo necessário para viajar pela rede é diretamente proporcional ao tamanho dos arquivos.

Assim, reduzir o tamanho dos recursos externos e usar apenas recursos absolutamente necessários é o método preferido para melhorar o desempenho dos formulários. Você pode executar as seguintes otimizações em um formulário XFA para reduzir o tamanho dos recursos externos de um formulário:

* Usar [imagens compactadas](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Reduz a atividade de rede e a quantidade de memória necessária para renderizar um formulário. Portanto, o tempo de carregamento do formulário diminui substancialmente.
* Use a opção de minificação no Gerenciador de configuração do AEM (Gerenciador de biblioteca HTML Day CQ) para compactar arquivos JavaScript e CSS. Para obter detalhes, consulte [Configurações de OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Habilitar compactação da Web. Reduz o tamanho das solicitações e respostas originadas de um formulário. Para obter detalhes, consulte [Ajuste de desempenho do AEM Forms Server](https://helpx.adobe.com/br/aem-forms/6-3/performance-tuning-aem-forms.html).

## Manter o interesse ativo, mostrar apenas campos obrigatórios  {#keep-the-interest-alive-show-only-required-fields}

Um formulário HTML5 pode ser executado em centenas de páginas. É lento carregar um formulário com um grande número de campos no navegador. Você pode executar as seguintes otimizações em um formulário XFA para otimizar os formulários com um grande número de campos e páginas:

* Avaliar a divisão de formulários grandes em vários formulários. Também é possível usar um conjunto de formulários para agrupar todos os formulários menores e apresentá-los como uma única unidade. Um conjunto de formulários carrega somente formulários necessários. Além disso, em um conjunto de formulários, é possível configurar campos comuns em diferentes formulários para compartilhar associações de dados. As vinculações de dados ajudam os usuários a preencher informações comuns apenas uma vez; as informações são preenchidas automaticamente em formulários subsequentes, resultando em melhorias substanciais de desempenho. Para obter mais detalhes sobre conjuntos de formulários, consulte [Conjunto de formulários em formulários AEM](https://helpx.adobe.com/br/aem-forms/6-3/formset-in-aem-forms.html).
* Considere dividir seções e mover cada seção para uma página diferente. Os formulários HTML5 carregam dinamicamente cada página na solicitação de rolagem de página. Somente as páginas roladas (a página que está sendo exibida e as páginas que a precedem) são armazenadas na memória; o restante das páginas é carregado sob demanda. Assim, dividir e mover uma seção em uma página própria reduz o tempo necessário para carregar um formulário. Você também pode usar a primeira página do formulário como página inicial. É semelhante ao índice de um livro. Uma landing page do formulário contém apenas links para as outras seções do formulário. Ele melhora significativamente o tempo de carregamento da primeira página do formulário e resulta em uma experiência do usuário aprimorada.
* Mantenha as seções condicionais ocultas, por padrão. Torne essas seções visíveis somente quando uma determinada condição for atendida. Ajuda a manter o tamanho do DOM no mínimo. Também é possível usar a navegação com guias para exibir apenas uma seção por vez.

## Menos é mais, reduza o número de páginas {#less-is-more-reduce-the-number-of-pages}

Os formulários HTML5 podem conter campos orientados por dados (tabelas e subformulários). Esses campos expandem o tamanho do formulário no tempo de execução. Por exemplo, uma tabela orientada por dados em um formulário HTML5 pode abranger milhares de linhas. Essas tabelas podem causar degradação do layout e do desempenho. As otimizações sugeridas abaixo podem ajudar a reduzir o tempo de carregamento dos formulários HTML5 com campos orientados por dados:

* Use scripts XFA para obter uma navegação paginada e exibir campos orientados por dados (tabelas e subformulários). Na navegação paginada, somente dados específicos são exibidos em uma página. Limita a operação de pintura do navegador aos campos que estão sendo exibidos de cada vez e facilita a navegação em um formulário. Além disso, os usuários dos dispositivos móveis estão interessados apenas em um subconjunto de dados. Ele ajuda a fornecer uma excelente experiência ao usuário e reduz o tempo necessário para carregar os dados necessários. Você tem duas soluções pelo preço de uma.  Observe também que a navegação paginada não está disponível imediatamente. Você pode usar scripts XFA para desenvolver a navegação paginada.

* Avaliar a mesclagem de várias colunas somente leitura em uma única coluna. Ele reduz a memória necessária para exibir a forma. Além disso, evite exibir as colunas que não exigem entradas dos usuários.
* Avalie a divisão do formulário orientado por dados em um [conjunto de formulários](https://helpx.adobe.com/br/aem-forms/6-3/formset-in-aem-forms.html), se as sugestões acima não resultarem em muitas melhorias. Por exemplo, se uma tabela tiver mais de 1000 linhas, mova cada 100 linhas para um formulário diferente. Isso ajudaria a melhorar o tempo de carregamento e o desempenho dos formulários.  Observe também que um conjunto de formulários produz um XML de envio consolidado para todos os formulários. Para diferenciar os dados de cada formulário, use raízes de dados diferentes. Para obter mais informações, consulte [Conjunto de formulários no AEM Forms](https://helpx.adobe.com/br/aem-forms/6-3/formset-in-aem-forms.html).

## Poder de dois para documento de registro (DOR) {#power-of-two-for-document-of-record-dor}

Um formulário XFA pode ter várias seções dedicadas apenas ao Documento de registro (DOR). Para reduzir o número de nós e melhorar o desempenho desse formulário, você pode manter diferentes cópias do formulário: uma cópia para preencher o formulário e outra para gerar o Documento de registro no servidor. Na cópia a ser preenchida com o formulário XFA, exiba os campos necessários somente para capturar dados. No XFA de gerar documento de registro de, mantenha os campos obrigatórios somente na saída impressa do formulário. Antes de escolher a abordagem sugerida, avalie o ganho de desempenho e o overhead de manutenção.

## Leituras recomendadas  {#recommended-reads}

Os formulários Adobe Experience Manager (AEM) podem ajudar você a transformar transações complexas em experiências digitais simples e atraentes. No entanto, exige um esforço concertado para desenvolver formas eficientes e produtivas. Além do HTML5 Forms, aqui estão algumas leituras recomendadas para as práticas recomendadas gerais do AEM:

* [Práticas recomendadas para implantação e manutenção do AEM](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas para criação de conteúdo](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas para administração de AEM](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas para o desenvolvimento de soluções](/help/sites-developing/best-practices.md)
* [Práticas recomendadas para trabalhar com formulários adaptáveis](/help/forms/using/adaptive-forms-best-practices.md)
* [O servidor AEM Forms não incorpora fontes a um formulário de PDF Dinâmico](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Cartão de referência rápida {#quick-reference-card}

Você pode imprimir o seguinte cartão (clique no cartão para baixar uma versão de alta resolução) e mantê-lo em sua mesa para uma referência rápida:
[![cartão de referência rápida de práticas recomendadas do HTML5 da Forms](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
